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

    static int N, K, M;
    static long[] ans;
    static List<int[]> Edges;
    static TreeMap<Integer, Long>[] S;
    static int[] r;

    static int f(int x) { return x==r[x] ? x : (r[x]=f(r[x])); }

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    public static void init() throws Exception {

        N = io.nextInt();
        K = io.nextInt();
        M = io.nextInt();

        r = new int[N+1];
        S = new TreeMap[N+1];
        for(int i=1;i<=N;i++) {
            S[i] = new TreeMap<>();
            S[i].put(io.nextInt(), 1L);
            r[i] = i;
        }

        Edges = new ArrayList<>();
        for(int i=0;i<M;i++) {
            int a = io.nextInt(), b = io.nextInt(), c = io.nextInt();
            Edges.add(new int[]{a,b,c});
        }

        ans = new long[K+1];

    }

    static void solve() throws Exception {

        Collections.sort(Edges, (a,b) -> b[2]-a[2]);
        for(int[] e:Edges) {
            int a = e[0], b = e[1], c = e[2];

            int x = f(a), y = f(b);
            if(x == y) continue;
            int small = x, large = y;
            if(S[x].size() > S[y].size()){
                small = y;
                large = x;
            }

            for(int key : S[small].keySet()) {
                ans[key] += S[large].getOrDefault(key, 0L) * S[small].get(key) * c;
                S[large].put(key, S[large].getOrDefault(key, 0L) + S[small].get(key));
            }
            S[small] = new TreeMap<>();
            r[small] = large;

        }

        for(int i=1;i<=K;i++) io.write(ans[i] + "\n");

    }

}
```
