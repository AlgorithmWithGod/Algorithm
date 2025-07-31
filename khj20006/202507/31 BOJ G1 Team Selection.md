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
    static int[][] arr;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    static void init() throws Exception {

        N = io.nextInt();
        arr = new int[N+1][];
        for(int i=1;i<=N;i++) arr[i] = new int[]{io.nextInt(),io.nextInt(),io.nextInt(),io.nextInt(),io.nextInt()};

    }

    static void solve() throws Exception {

        int[] dp = new int[32];
        for(int i=1;i<=N;i++) {
            int[] ndp = new int[32];
            for(int j=0;j<32;j++) ndp[j] = dp[j];
            for(int j=0;j<5;j++) for(int k=0;k<32;k++) if((k & (1<<j)) != 0) {
                ndp[k] = Math.max(ndp[k], dp[k^(1<<j)] + arr[i][j]);
            }
            dp = ndp;
        }
        io.write(dp[31] + "\n");

    }

}
```
