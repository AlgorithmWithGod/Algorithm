```java
import java.util.*;
import java.io.*;

class IOController {
    BufferedReader br;
    BufferedWriter bw;
    StringTokenizer st;

    public IOController() {
        br = new BufferedReader(new InputStreamReader(System.in));
        bw = new BufferedWriter(new OutputStreamWriter(System.out));
        st = new StringTokenizer("");
    }

    String nextLine() throws Exception {
        String line = br.readLine();
        st = new StringTokenizer(line);
        return line;
    }

    String nextToken() throws Exception {
        while (!st.hasMoreTokens()) nextLine();
        return st.nextToken();
    }

    int nextInt() throws Exception {
        return Integer.parseInt(nextToken());
    }

    long nextLong() throws Exception {
        return Long.parseLong(nextToken());
    }

    double nextDouble() throws Exception {
        return Double.parseDouble(nextToken());
    }

    void close() throws Exception {
        bw.flush();
        bw.close();
    }

    void write(String content) throws Exception {
        bw.write(content);
    }

}

public class Main {

    static IOController io;

    //

    static int N, M;
    static int[] cost;
    static List<int[]>[] graph;
    static List<int[]> edges;
    static int[] r, depth;
    static int[][] parent, min;

    public static int f(int x) {return x==r[x] ? x : (r[x]=f(r[x]));}

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    public static void init() throws Exception {

        N = io.nextInt();
        M = io.nextInt();
        cost = new int[N];
        for(int i=0;i<N;i++) cost[i] = io.nextInt();
        graph = new List[N*N];
        r = new int[N*N];
        depth = new int[N*N];
        parent = new int[N*N+1][18];
        min = new int[N*N+1][18];
        for(int i=0;i<N*N;i++) {
            graph[i] = new ArrayList<>();
            r[i] = i;
            int x = i/N, y = i%N;
        }
        edges = new ArrayList<>();
        while(M-->0) {
            int u = io.nextInt() - 1;
            int v = io.nextInt() - 1;
            for(int i=0;i<N;i++) {
                int from = i*N + u;
                int to = i*N + v;
                int value = cost[i] * Math.max(cost[u], cost[v]);
                edges.add(new int[]{from, to, value});

                from = u*N + i;
                to = v*N + i;
                edges.add(new int[]{from, to, value});
            }
        }

    }

    static void solve() throws Exception {

        constructMST();
        dfs(0, N*N, 0);
        constructSparseTable();

        int Q = io.nextInt();
        while(Q-->0) {
            int u = io.nextInt() - 1;
            int v = io.nextInt() - 1;
            int from = u*N + v;
            int to = v*N + u;

            io.write(getMinValue(from, to) + "\n");
        }

    }

    static void constructMST() {
        Collections.sort(edges, (a,b) -> a[2]-b[2]);
        for(int[] edge : edges) {
            int a = edge[0], b = edge[1], c = edge[2];
            int x = f(a), y = f(b);
            if(x == y) continue;
            r[x] = y;
            graph[a].add(new int[]{b,c});
            graph[b].add(new int[]{a,c});
        }
    }

    static void dfs(int n, int p, int d) {
        depth[n] = d;
        parent[n][0] = p;
        for(int[] e:graph[n]) if(e[0] != p) {
            dfs(e[0], n, d+1);
            min[e[0]][0] = e[1];
        }
    }

    static void constructSparseTable() {
        for(int k=1;k<18;k++) for(int i=0;i<N*N;i++) {
            parent[i][k] = parent[parent[i][k-1]][k-1];
            min[i][k] = Math.max(min[i][k-1], min[parent[i][k-1]][k-1]);
        }
    }

    static int getMinValue(int a, int b) {
        int depthDiff = Math.abs(depth[a] - depth[b]);
        int result = 0;
        for(int k=0;k<18;k++) if((depthDiff & (1<<k)) != 0) {
            if(depth[a] > depth[b]) {
                result = Math.max(result, min[a][k]);
                a = parent[a][k];
            }
            else {
                result = Math.max(result, min[b][k]);
                b = parent[b][k];
            }
        }

        for(int k=17;k>=0;k--) if(parent[a][k] != parent[b][k]) {
            result = Math.max(result, Math.max(min[a][k], min[b][k]));
            a = parent[a][k];
            b = parent[b][k];
        }
        if(a != b) {
            result = Math.max(result, Math.max(min[a][0], min[b][0]));
        }

        return result;

    }

}
```
