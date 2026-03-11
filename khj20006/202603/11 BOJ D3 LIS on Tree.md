```java
import java.io.*;
import java.util.*;

public class BOJ33752 {

    static class SegmentTree {
        int[] tree;
        SegmentTree(int size) {
            tree = new int[size*4];
        }

        void update(int s, int e, int i, int v, int n) {
            if(s == e) {
                tree[n] = v;
                return;
            }
            int m = (s+e) >> 1;
            if(i <= m) {
                update(s, m, i, v, n*2);
            }
            else {
                update(m+1, e, i, v, n*2+1);
            }
            tree[n] = Math.max(tree[n*2], tree[n*2+1]);
        }

        int find(int s, int e, int l, int r, int n) {
            if(l > r || l > e || r < s) return 0;
            if(l <= s && e <= r) return tree[n];
            int m = (s+e) >> 1;
            return Math.max(find(s, m, l, r, n*2), find(m+1, e, l, r, n*2+1));
        }
    }

    static class Choice {
        int value, index;
        Choice(int value, int index) {
            this.value = value;
            this.index = index;
        }
    }

    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;

    static int N;
    static List<Integer>[] graph;
    static int[][] infos;
    static int[] arr, in, out, parent;
    static Choice[] dec, asc, dec2, asc2;
    static int order = 0;
    static SegmentTree seg;

    static List<Integer>[] ascLists, decLists;

    public static void main(String[] args) throws Exception {
        // 0. Input

        N = Integer.parseInt(br.readLine());
        arr = new int[N+1];
        infos = new int[N][2];
        graph = new List[N+1];

        st = new StringTokenizer(br.readLine());
        for(int i=1;i<=N;i++) {
            graph[i] = new ArrayList<>();
            arr[i] = Integer.parseInt(st.nextToken());
            infos[i-1][0] = arr[i];
            infos[i-1][1] = i;
        }

        for(int i=1;i<N;i++) {
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            graph[a].add(b);
            graph[b].add(a);
        }

        int answer = solve(1);

        bw.write(answer + "\n");
        bw.close();
    }

    public static int solve(int root) throws Exception {
        // 1. Euler-Tour Technique

        in = new int[N+1];
        out = new int[N+1];
        parent = new int[N+1];
        order = 0;
        dfs(root, 0);

        // 2. Segment Tree

        /// 2-1. LIS : leaf -> root

        asc = new Choice[N+1];
        asc2 = new Choice[N+1];
        Arrays.sort(infos, (a, b) -> Integer.compare(a[0], b[0]));
        longestSubsequenceDP(infos, asc, asc2);

        /// 2-2. LDS : leaf -> root

        dec = new Choice[N+1];
        dec2 = new Choice[N+1];
        Arrays.sort(infos, (a, b) -> Integer.compare(b[0], a[0]));
        longestSubsequenceDP(infos, dec, dec2);

        // 3. Find Answer

        /// Case 1) LIS contains LCA, 2nd best dp

        int answer = 1;
        for(int i=1;i<=N;i++) {
            if(dec[i].index == asc[i].index) {
                answer = Math.max(answer, Math.max(dec[i].value + asc2[i].value - 1, dec2[i].value + asc[i].value - 1));
                answer = Math.max(answer, Math.max(dec[i].value, asc[i].value));
            }
            else {
                answer = Math.max(answer, dec[i].value + asc[i].value - 1);
            }
        }

        /// Case 2) LIS doesn't contains LCA, Smaller To Larger

        ascLists = new List[N+1];
        decLists = new List[N+1];
        for(int i=1;i<=N;i++) {
            ascLists[i] = new ArrayList<>();
            decLists[i] = new ArrayList<>();
        }

        answer = Math.max(answer, dfs2(1, 0));

        return answer;
    }

    public static void dfs(int cur, int par) {
        in[cur] = ++order;
        parent[cur] = par;
        for(int nxt : graph[cur]) if(nxt != par) {
            dfs(nxt, cur);
        }
        out[cur] = order;
    }

    public static void longestSubsequenceDP(int[][] arr, Choice[] ch1, Choice[] ch2) {
        seg = new SegmentTree(N);
        for(int i=1;i<=N;i++) {
            ch1[i] = new Choice(1, 0);
            ch2[i] = new Choice(1, -1);
        }
        for(int i=0;i<N;) {
            int curValue = arr[i][0];
            List<Integer> updates = new ArrayList<>();
            while(i<N && arr[i][0] == curValue) {
                int curIndex = arr[i][1];
                for(int child : graph[curIndex]) if(child != parent[curIndex]) {
                    int result = seg.find(1, N, in[child], out[child], 1) + 1;
                    if(result > ch1[curIndex].value) {
                        ch2[curIndex] = ch1[curIndex];
                        ch1[curIndex] = new Choice(result, child);
                    }
                    else if(result > ch2[curIndex].value) {
                        ch2[curIndex] = new Choice(result, child);
                    }
                }
                updates.add(curIndex);
                i++;
            }

            for(int node : updates) {
                seg.update(1, N, in[node], ch1[node].value, 1);
            }
        }
    }

    public static int dfs2(int cur, int par) {
        int ret = 0;
        for(int nxt : graph[cur]) if(nxt != par) {
            ret = Math.max(ret, dfs2(nxt, cur));

            if (ascLists[nxt].size() + decLists[nxt].size() > ascLists[cur].size() + decLists[cur].size()) {
                List<Integer> temp1 = ascLists[nxt];
                ascLists[nxt] = ascLists[cur];
                ascLists[cur] = temp1;
                List<Integer> temp2 = decLists[nxt];
                decLists[nxt] = decLists[cur];
                decLists[cur] = temp2;
            }

            for(int i=0;i<ascLists[nxt].size();i++) {
                int nxtVal = ascLists[nxt].get(i);

                int s = -1, e = decLists[cur].size()-1, m = (s+e+1)>>1;
                while(s < e) {
                    int curr = decLists[cur].get(m);
                    if(curr > nxtVal) {
                        s = m;
                    }
                    else {
                        e = m-1;
                    }
                    m = (s+e+1)>>1;
                }
                ret = Math.max(ret, m+i+2);
            }

            for(int i=0;i<decLists[nxt].size();i++) {
                int nxtVal = decLists[nxt].get(i);

                int s = -1, e = ascLists[cur].size()-1, m = (s+e+1)>>1;
                while(s < e) {
                    int curr = ascLists[cur].get(m);
                    if(curr < nxtVal) {
                        s = m;
                    }
                    else {
                        e = m-1;
                    }
                    m = (s+e+1)>>1;
                }
                ret = Math.max(ret, i+m+2);
            }

            for(int i=0;i<ascLists[nxt].size();i++) {
                if(i >= ascLists[cur].size()) {
                    ascLists[cur].add((int)1e9 + 7);
                }
                int curVal = ascLists[cur].get(i);
                int nxtVal = ascLists[nxt].get(i);
                if(nxtVal < curVal) {
                    ascLists[cur].set(i, nxtVal);
                }
            }

            for(int i=0;i<decLists[nxt].size();i++) {
                if(i >= decLists[cur].size()) {
                    decLists[cur].add(0);
                }
                int curVal = decLists[cur].get(i);
                int nxtVal = decLists[nxt].get(i);
                if(nxtVal > curVal) {
                    decLists[cur].set(i, nxtVal);
                }
            }

        }

        if(ascLists[cur].size() + 1 == asc[cur].value) {
            ascLists[cur].add(arr[cur]);
        }
        else {
            ascLists[cur].set(asc[cur].value-1, arr[cur]);
        }

        if(decLists[cur].size() + 1 == dec[cur].value) {
            decLists[cur].add(arr[cur]);
        }
        else {
            decLists[cur].set(dec[cur].value-1, arr[cur]);
        }

        return ret;
    }
}
```
