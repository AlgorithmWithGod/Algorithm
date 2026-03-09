```java
import java.io.*;
import java.util.*;

public class BOJ13892 {

    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;

    static int N, Q;
    static List<int[]>[] graph;
    static int[][] queries;

    static List<Integer>[] chains, mergeSortTree;
    static int[] chainNum, chainIdx, depth, size, parent, order, reverseOrder, arr;
    static int orderCnt = 0;

    public static void main(String[] args) throws Exception {
        int T = Integer.parseInt(br.readLine());
        while(T-- > 0) {
            N = Integer.parseInt(br.readLine());
            graph = new List[N+1];
            for(int i=1;i<=N;i++) {
                graph[i] = new ArrayList<>();
            }

            for(int i=1;i<N;i++) {
                st = new StringTokenizer(br.readLine());
                int a = Integer.parseInt(st.nextToken());
                int b = Integer.parseInt(st.nextToken());
                int c = Integer.parseInt(st.nextToken());
                graph[a].add(new int[]{b,c});
                graph[b].add(new int[]{a,c});
            }

            Q = Integer.parseInt(br.readLine());
            queries = new int[Q][];
            for(int i=0;i<Q;i++) {
                st = new StringTokenizer(br.readLine());
                int a = Integer.parseInt(st.nextToken());
                int b = Integer.parseInt(st.nextToken());
                queries[i] = new int[]{a,b};
            }

            solve();
        }
        bw.close();
    }

    public static void solve() throws Exception {
        // 1. Initialize

        chains = new List[N+1];
        for(int i=1;i<=N;i++) {
            chains[i] = new ArrayList<>();
        }
        chainNum = new int[N+1];
        chainIdx = new int[N+1];
        depth = new int[N+1];
        size = new int[N+1];
        parent = new int[N+1];
        order = new int[N+1];
        reverseOrder = new int[N+1];
        arr = new int[N+1];

        // 1-1. Heavy-Light Decomposition

        dfs(1, 0);
        orderCnt = 0;
        hld(1, 0, 1, 0);

        // 1-2. Merge Sort Tree

        mergeSortTree = new List[4*N];
        for(int i=1;i<4*N;i++) {
            mergeSortTree[i] = new ArrayList<>();
        }

        init(1, N, 1);

        // 2. Solve

        for(int[] query : queries) {
            int a = query[0], b = query[1];

            // 2-1. Find LCA & path distance
            int dist = pathDistance(a, b);

            // 2-2. Find median of path
            int median = kthValueOnPath(a, b, (dist+1) / 2);
            if(dist % 2 == 0) {
                median += kthValueOnPath(a, b, dist/2 + 1);
            }

            // 2-3. Print result
            if(dist % 2 == 0) {
                bw.write((median/2) + "." + ((median%2)*5) + "\n");
            }
            else {
                bw.write(median + ".0\n");
            }

        }
    }

    public static void dfs(int cur, int par) {
        parent[cur] = par;
        size[cur] = 1;
        for(int[] edge : graph[cur]) if(edge[0] != par) {
            dfs(edge[0], cur);
            arr[edge[0]] = edge[1];
            size[cur] += size[edge[0]];
        }
    }

    public static void hld(int cur, int par, int chainRoot, int dep) {
        depth[cur] = dep;
        chainNum[cur] = chainRoot;
        chainIdx[cur] = chains[chainRoot].size();
        chains[chainRoot].add(cur);
        order[cur] = ++orderCnt;
        reverseOrder[orderCnt] = cur;
        int h = -1;
        for(int[] edge : graph[cur]) if(edge[0] != par && (h == -1 || size[edge[0]] > size[h])) {
            h = edge[0];
        }
        if(h != -1) {
            hld(h, cur, chainRoot, dep);
        }
        for(int[] edge : graph[cur]) if(edge[0] != par && edge[0] != h) {
            hld(edge[0], cur, edge[0], dep + 1);
        }
    }

    public static int pathDistance(int a, int b) {
        int len = 0;
        while(chainNum[a] != chainNum[b]) {
            if(depth[a] > depth[b]) {
                len += chainIdx[a] + 1;
                a = parent[chainNum[a]];
            }
            else {
                len += chainIdx[b] + 1;
                b = parent[chainNum[b]];
            }
        }
        return len + Math.abs(chainIdx[a] - chainIdx[b]);
    }

    public static void init(int s, int e, int n) {
        if(s == e) {
            mergeSortTree[n].add(arr[reverseOrder[s]]);
            return;
        }
        int m = (s+e) >> 1;
        init(s, m, n*2);
        init(m+1, e, n*2+1);

        int p1 = 0, p2 = 0;
        while(p1 < mergeSortTree[n*2].size() && p2 < mergeSortTree[n*2+1].size()) {
            int v1 = mergeSortTree[n*2].get(p1);
            int v2 = mergeSortTree[n*2+1].get(p2);
            if(v1 < v2) {
                mergeSortTree[n].add(v1);
                p1++;
            }
            else {
                mergeSortTree[n].add(v2);
                p2++;
            }
        }

        while(p1 < mergeSortTree[n*2].size()) {
            mergeSortTree[n].add(mergeSortTree[n*2].get(p1++));
        }
        while(p2 < mergeSortTree[n*2+1].size()) {
            mergeSortTree[n].add(mergeSortTree[n*2+1].get(p2++));
        }
    }

    public static int countLeqThanK(int s, int e, int l, int r, int k, int n) {
        if(l > r || l > e || r < s) return 0;
        if(l <= s && e <= r) {
            int lo = 0, hi = mergeSortTree[n].size(), mid = (lo + hi) >> 1;
            while(lo < hi) {
                if(mergeSortTree[n].get(mid) <= k) {
                    lo = mid + 1;
                }
                else {
                    hi = mid;
                }
                mid = (lo + hi) >> 1;
            }
            return mid;
        }
        int m = (s+e) >> 1;
        return countLeqThanK(s, m, l, r, k, n*2) + countLeqThanK(m+1, e, l, r, k, n*2+1);
    }

    public static int kthValueOnPath(int a, int b, int k) {
        int s = 1, e = 100_000, m = (s+e) >> 1;
        while(s < e) {
            if(countOnPathLeqThanK(a, b, m) < k) {
                s = m + 1;
            }
            else {
                e = m;
            }
            m = (s+e) >> 1;
        }
        return m;
    }

    public static int countOnPathLeqThanK(int a, int b, int k) {
        int ret = 0;

        while(chainNum[a] != chainNum[b]) {
            if(depth[a] > depth[b]) {
                ret += countLeqThanK(1, N, order[chainNum[a]], order[a], k, 1);
                a = parent[chainNum[a]];
            }
            else {
                ret += countLeqThanK(1, N, order[chainNum[b]], order[b], k, 1);
                b = parent[chainNum[b]];
            }
        }
        if(chainIdx[a] > chainIdx[b]) {
            ret += countLeqThanK(1, N, order[b]+1, order[a], k, 1);
        }
        else {
            ret += countLeqThanK(1, N, order[a]+1, order[b], k, 1);
        }

        return ret;
    }
}
```
