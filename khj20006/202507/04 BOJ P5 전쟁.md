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

    static final int INF = (int)1e9 + 7;

    static int N, M;
    static String[] A;
    static HashMap<String, Integer> deg;
    static HashMap<String, List<String>> V;
    static HashMap<String, Integer> C;
    static HashMap<String, Integer> S;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    public static void init() throws Exception {

        N = io.nextInt();
        M = io.nextInt();
        A = new String[N];
        deg = new HashMap<>();
        V = new HashMap<>();
        C = new HashMap<>();
        S = new HashMap<>();
        for(int i=0;i<N;i++) {
            String line = io.nextLine();
            String[] arr = line.split(" ");
            String a = arr[0];
            int c = Integer.parseInt(arr[1]);
            C.put(a,c);
            A[i] = a;
            V.put(a, new ArrayList<>());
            if(arr.length >= 3) {
                for(int k=2;k<arr.length;k++) {
                    String b = arr[k];
                    V.get(a).add(b);
                    deg.put(b, 1);
                }
            }
        }

    }

    static void solve() throws Exception {

        int[] dp = new int[N+1];
        Arrays.fill(dp, INF);
        dp[0] = 0;
        for(int i=0;i<N;i++) if(deg.getOrDefault(A[i], 0) == 0) {
            int[] res = dfs(A[i]);
            int[] ndp = new int[N+1];
            for(int k=0;k<=N;k++) ndp[k] = dp[k];
            for(int k=N;k>0;k--) if(res[k] != INF) {
                for(int j=N;j>=k;j--) if(dp[j-k] != INF) ndp[j] = Math.min(ndp[j], dp[j-k] + res[k]);
            }
            for(int k=0;k<=N;k++) dp[k] = ndp[k];
        }

        int ans = INF;
        for(int i=M;i<=N;i++) ans = Math.min(ans, dp[i]);
        io.write(ans + "\n");

    }

    static int[] dfs(String n) {
        int child = 1;
        int[] dp = new int[N+1];
        Arrays.fill(dp, INF);
        dp[0] = 0;
        for(String i : V.getOrDefault(n, new ArrayList<>())) {
            int[] res = dfs(i);
            child += S.get(i);
            int[] ndp = new int[N+1];
            for(int k=0;k<=N;k++) ndp[k] = dp[k];
            for(int k=N;k>0;k--) if(res[k] != INF) {
                for(int j=N;j>=k;j--) if(dp[j-k] != INF) ndp[j] = Math.min(ndp[j], dp[j-k] + res[k]);
            }
            for(int k=0;k<=N;k++) dp[k] = ndp[k];
        }
        dp[child] = Math.min(dp[child], C.get(n));

        S.put(n, child);
        return dp;
    }

}
```
