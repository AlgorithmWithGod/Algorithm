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

    static final long INF = -(long)1e18 + 7;

    static int N, M, A, B;
    static int[] earn;
    static List<int[]> edges;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    public static void init() throws Exception {

        N = io.nextInt();
        A = io.nextInt();
        B = io.nextInt();
        M = io.nextInt();
        edges = new ArrayList<>();
        for(int i=0;i<M;i++){
            int a = io.nextInt();
            int b = io.nextInt();
            int c = io.nextInt();
            edges.add(new int[] {a,b,c});
        }
        earn = new int[N];
        for(int i=0;i<N;i++) earn[i] = io.nextInt();

    }

    static void solve() throws Exception {

        boolean[] fromA = new boolean[N];
        boolean[] toB = new boolean[N];
        Queue<Integer> q = new ArrayDeque<>();
        boolean[] vis = new boolean[N];
        q.add(A);
        vis[A] = true;
        while(!q.isEmpty()){
            int cur = q.poll();
            fromA[cur] = true;
            for(int[] edge: edges) if(edge[0] == cur) {
                if(!vis[edge[1]]) {
                    q.add(edge[1]);
                    vis[edge[1]] = true;
                }
            }
        }

        for(int i=0;i<N;i++) {
            vis = new boolean[N];
            q.add(i);
            vis[i] = true;
            while(!q.isEmpty()){
                int cur = q.poll();
                if(cur == B) toB[i] = true;
                for(int[] edge:edges) if(edge[0] == cur) {
                    if(!vis[edge[1]]) {
                        q.add(edge[1]);
                        vis[edge[1]] = true;
                    }
                }
            }
        }

        long[] dist = new long[N];
        Arrays.fill(dist, INF);
        dist[A] = -earn[A];
        for(int step=1;step<=N;step++) {
            long before = dist[A];
            for(int[] edge:edges) {
                int from = edge[0], to = edge[1], cost = edge[2];
                if(dist[from] != INF && (dist[to] == INF || dist[to] > dist[from] + cost - earn[to])) {
                    dist[to] = dist[from] + cost - earn[to];
                    if(step == N && fromA[to] && toB[to]) {
                        io.write("Gee");
                        return;
                    }
                }
            }
        }

        if(dist[B] == INF) io.write("gg");
        else io.write(-dist[B] + "\n");

    }

}
```
