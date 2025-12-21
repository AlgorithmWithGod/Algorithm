```java
import java.util.*;
import java.io.*;

class DisjointSet {
    int[] root, cnt;
    Stack<int[]> works;
    DisjointSet(int size) {
        root = new int[size];
        cnt = new int[size];
        for(int i=0;i<size;i++) {
            root[i] = i;
            cnt[i] = 1;
        }
        works = new Stack<>();
    }

    int find(int x) { return x == root[x] ? x : find(root[x]); }

    void union(int a, int b) {
        int x = find(a), y = find(b);
        if(x == y) {
            works.push(new int[]{-1,-1,-1});
            return;
        }
        if(cnt[x] > cnt[y]) {
            int temp = x;
            x = y;
            y = temp;
        }
        works.push(new int[]{x, y, cnt[x]});
        cnt[y] += cnt[x];
        root[x] = y;
    }

    void rollback() {
        if(!works.empty()) {
            int[] info = works.pop();
            int x = info[0], y = info[1], c = info[2];
            if(x != -1) {
                root[x] = x;
                cnt[y] -= c;
            }
        }
    }
}

public class Main {

    static BufferedReader br;
    static BufferedWriter bw;
    static StringTokenizer st;

    static int N, K;
    static List<int[]>[] edges;
    static int[][] finds;
    static Map<String, Integer> edgeTime;
    static DisjointSet ds;

    public static void main(String[] args) throws Exception {
        bw = new BufferedWriter(new OutputStreamWriter(System.out));

        input();
        solve();

        bw.close();
    }

    public static void input() throws Exception {
        br = new BufferedReader(new InputStreamReader(System.in));

        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());
        edges = new List[4*K];
        finds = new int[K+1][2];
        for(int i=1;i<=K;i++) finds[i] = new int[]{-1,-1};
        for(int i=1;i<4*K;i++) edges[i] = new ArrayList<>();
        edgeTime = new TreeMap<>();
        for(int i=1;i<=K;i++) {
            st = new StringTokenizer(br.readLine());
            int op = Integer.parseInt(st.nextToken());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            if(op == 3) finds[i] = new int[]{a,b};
            else {
                if(op == 1) edgeTime.put(a + " " + b, i);
                else {
                    int start = edgeTime.get(a + " " + b);
                    edgeTime.remove(a + " " + b);
                    update(1,K,start,i,a,b,1);
                }
            }
        }
        for(String key : edgeTime.keySet()) {
            int start = edgeTime.get(key);
            String[] sp = key.split(" ");
            int a = Integer.parseInt(sp[0]);
            int b = Integer.parseInt(sp[1]);
            update(1,K,start,K,a,b,1);
        }

        br.close();
    }

    public static void update(int s, int e, int l, int r, int a, int b, int n) {
        if(l>r || l>e || r<s) return;
        if(l<=s && e<=r) {
            edges[n].add(new int[]{a, b});
            return;
        }
        int m = (s+e)>>1;
        update(s,m,l,r,a,b,n*2);
        update(m+1,e,l,r,a,b,n*2+1);
    }

    public static void solve() throws Exception {
        ds = new DisjointSet(N);
        dnc(1,K,1);
    }

    public static void dnc(int s, int e, int n) throws Exception {
        for(int[] edge : edges[n]) {
            int a = edge[0], b = edge[1];
            ds.union(a,b);
        }

        if(s == e) {
            if(finds[s][0] != -1) {
                int a = finds[s][0], b = finds[s][1];
                boolean result = ds.find(a) == ds.find(b);
                bw.write(result ? "YES\n" : "NO\n");
            }
        }
        else {
            int m = (s+e)>>1;
            dnc(s,m,n*2);
            dnc(m+1,e,n*2+1);
        }

        for(int[] edge : edges[n]) {
            ds.rollback();
        }
    }

}
```
