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

    static int N;
    static int[] A;
    static int[][] dp;
    static List<Integer>[] V;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    public static void init() throws Exception {

        N = io.nextInt();
        A = new int[N+1];
        V = new List[N+1];
        for(int i=1;i<=N;i++) V[i] = new ArrayList<>();
        for(int i=2;i<=N;i++) V[io.nextInt()].add(i);
        for(int i=1;i<=N;i++) A[i] = io.nextInt();
        dp = new int[N+1][2];

    }

    static void solve() throws Exception {

        dfs(1);
        io.write(Math.max(dp[1][0], dp[1][1]) + "\n");

    }

    static void dfs(int n) {
        for(int i:V[n]) {
            dfs(i);
            dp[n][0] += Math.max(dp[i][0], dp[i][1]);
        }
        int max = Integer.MIN_VALUE;
        for(int i:V[n]) {
            max = Math.max(max, -Math.max(dp[i][0], dp[i][1]) + dp[i][0] + A[i] * A[n]);
        }
        dp[n][1] = dp[n][0] + max;
    }

}
```
