```java
import java.util.*;
import java.io.*;

public class Main {

    static final int INF = (int)1e9 + 7;

    static BufferedReader br;
    static BufferedWriter bw;
    static StringTokenizer st;

    static int N, M, Q;
    static int[][] edges;
    static List<int[]>[] graph, tree;
    static int[] dep;
    static int[] root;
    static int[][] par, max, queries;
    static BitSet used;
    static int[] alternativeCost;

    public static int find(int x) { return x == root[x] ? x : (root[x] = find(root[x])); }

    public static void main(String[] args) throws Exception {

        input();
        solve();

    }

    public static void input() throws Exception {
        br = new BufferedReader(new InputStreamReader(System.in));

        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        edges = new int[M+1][];
        graph = new List[N+1];
        tree = new List[N+1];
        for(int i=1;i<=N;i++) {
            graph[i] = new ArrayList<>();
            tree[i] = new ArrayList<>();
        }

        for(int i=1;i<=M;i++) {
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            int c = Integer.parseInt(st.nextToken());
            edges[i] = new int[]{a,b,c};
            graph[a].add(new int[]{b,c});
            graph[b].add(new int[]{a,c});
        }

        Q = Integer.parseInt(br.readLine());
        queries = new int[Q][];
        for(int i=0;i<Q;i++) {
            st = new StringTokenizer(br.readLine());
            queries[i] = new int[]{Integer.parseInt(st.nextToken()), Integer.parseInt(st.nextToken())};
        }

        br.close();
    }

    public static void solve() throws Exception {
        // Construct MST
        root = new int[N+1];
        for(int i=1;i<=N;i++) root[i] = i;

        List<int[]> edgesTemp = new ArrayList<>();
        for(int i=1;i<=M;i++) edgesTemp.add(new int[]{edges[i][0], edges[i][1], edges[i][2], i});
        Collections.sort(edgesTemp, (a,b) -> a[2]-b[2]);

        int mstCost = 0;
        used = new BitSet(N+1);
        for(int[] edge : edgesTemp) {
            int a = edge[0], b = edge[1], c = edge[2], n = edge[3];
            int x = find(a), y = find(b);
            if(x == y) continue;
            mstCost += c;
            used.set(n);
            root[x] = y;
            tree[a].add(new int[]{b,c});
            tree[b].add(new int[]{a,c});
        }

        // Construct sparse table
        dep = new int[N+1];
        par = new int[N+1][17];
        max = new int[N+1][17];
        dfs(1,0,0);

        for(int k=1;k<17;k++) for(int i=1;i<=N;i++) {
            par[i][k] = par[par[i][k-1]][k-1];
            max[i][k] = Math.max(max[i][k-1], max[par[i][k-1]][k-1]);
        }

        // Find alternative cost
        root = new int[N+1];
        for(int i=1;i<=N;i++) root[i] = i;
        alternativeCost = new int[N+1];
        Arrays.fill(alternativeCost, INF);

        for(int[] edge : edgesTemp) if(!used.get(edge[3])) {
            int a = edge[0], b = edge[1], c = edge[2];
            int x = find(a), y = find(b);
            while(x != y) {
                if(dep[x] > dep[y]) {
                    alternativeCost[x] = c;
                    x = par[x][0];
                    root[x] = find(par[x][0]);
                    x = find(x);
                }
                else {
                    alternativeCost[y] = c;
                    y = par[y][0];
                    root[y] = find(par[y][0]);
                    y = find(y);
                }
            }
        }

        // Solve queries
        bw = new BufferedWriter(new OutputStreamWriter(System.out));
        bw.write(mstCost + "\n");

        for(int[] query : queries) {
            int a = edges[query[0]][0];
            int b = edges[query[0]][1];
            int c = query[1];

            if(used.get(query[0])) {
                int child = a == par[b][0] ? b : a;
                bw.write((mstCost - edges[query[0]][2] + Math.min(c, alternativeCost[child])) + "\n");
            }
            else {
                int mx = 0, diff = Math.abs(dep[a] - dep[b]);
                for(int k=0;k<17;k++) if((diff & (1<<k)) != 0) {
                    if(dep[a] > dep[b]) {
                        mx = Math.max(mx, max[a][k]);
                        a = par[a][k];
                    }
                    else {
                        mx = Math.max(mx, max[b][k]);
                        b = par[b][k];
                    }
                }

                for(int k=16;k>=0;k--) if(par[a][k] != par[b][k]) {
                    mx = Math.max(mx, Math.max(max[a][k], max[b][k]));
                    a = par[a][k];
                    b = par[b][k];
                }
                if(a != b) {
                    mx = Math.max(max[a][0], max[b][0]);
                }

                bw.write(Math.min(mstCost, mstCost + c - mx) + "\n");
            }

        }

        bw.close();
    }

    public static void dfs(int n, int p, int d) {
        par[n][0] = p;
        dep[n] = d;
        for(int[] edge : tree[n]) if(edge[0] != p) {
            dfs(edge[0], n, d+1);
            max[edge[0]][0] = edge[1];
        }
    }

}

```
