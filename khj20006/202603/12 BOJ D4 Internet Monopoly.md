```java
import java.io.*;
import java.util.*;

public class BOJ29851 {

    static class Query {
        int type, a, b;
        Query(int a) {
            this.type = 0;
            this.a = a;
        }
        Query(int a, int b) {
            this.type = 1;
            this.a = a;
            this.b = b;
        }
    }

    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;

    static int N, Q;
    static Query[] queries;
    static BitSet cantUnion;
    static List<Integer>[] tree;
    static int[] root, parent, depth;

    public static int find(int x) {
        return x == root[x] ? x : (root[x] = find(root[x]));
    }

    public static boolean union(int a, int b) {
        int x = find(a), y = find(b);
        if(x == y) return false;
        root[x] = y;
        return true;
    }

    public static void main(String[] args) throws Exception {
        // 0. Input + Construct Tree

        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        Q = Integer.parseInt(st.nextToken());

        queries = new Query[Q];
        cantUnion = new BitSet(Q);
        tree = new List[N+1];
        root = new int[N+1];
        for(int i=1;i<=N;i++) {
            root[i] = i;
            tree[i] = new ArrayList<>();
        }
        for(int i=0;i<Q;i++) {
            st = new StringTokenizer(br.readLine());
            if ("+".equals(st.nextToken())) {
                int a = Integer.parseInt(st.nextToken());
                int b = Integer.parseInt(st.nextToken());
                if(union(a,b)) {
                    tree[a].add(b);
                    tree[b].add(a);
                }
                else {
                    cantUnion.set(i);
                }
                queries[i] = new Query(a, b);
            }
            else {
                queries[i] = new Query(Integer.parseInt(st.nextToken()));
            }
        }

        // 1. DFS
        parent = new int[N+1];
        depth = new int[N+1];
        dfs(1, 0, 0);

        // 2. Count Non-bridge

        root = new int[N+1];
        for(int i=1;i<=N;i++) {
            root[i] = i;
        }
        int nonBridges = 0;
        for(int i=0;i<Q;i++) {
            Query query = queries[i];
            int type = query.type, a = query.a, b = query.b;
            if(type == 1) {
                if(!cantUnion.get(i)) continue;
                a = find(a);
                b = find(b);
                while(a != b) {
                    nonBridges++;
                    if(depth[a] > depth[b]) {
                        union(a, parent[a]);
                        a = find(parent[a]);
                    }
                    else {
                        union(b, parent[b]);
                        b = find(parent[b]);
                    }
                }
            }
            else {
                if(nonBridges <= a && a <= N-1) {
                    bw.write("JAH\n");
                }
                else {
                    bw.write("EI\n");
                }
            }
        }
        bw.close();
    }

    public static void dfs(int cur, int par, int dep) {
        parent[cur] = par;
        depth[cur] = dep;
        for(int nxt : tree[cur]) if(nxt != par) {
            dfs(nxt, cur, dep+1);
        }
    }

}
```
