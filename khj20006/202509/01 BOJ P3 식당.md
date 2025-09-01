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
    static int[] a;
    static int[][] dp, idx;
    static int[] min;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        N = io.nextInt();
        M = io.nextInt();
        a = new int[N+1];
        for(int i=1;i<=N;i++) a[i] = io.nextInt();
        dp = new int[N+1][201];
        idx = new int[N+1][201];
        min = new int[N+1];
        Arrays.fill(min, INF);
        min[0] = 0;

        for(int k=1;k<=200;k++) {
            int[] cnt = new int[M+1];
            int count = 0;
            for(int s=1,e=1;e<=N;e++) {
                if(cnt[a[e]]++ == 0) count++;
                while(count > k) {
                    if(--cnt[a[s++]] == 0) count--;
                }

                idx[e][k] = s;
            }
        }

        for(int i=1;i<=N;i++) {
            for(int k=1;k<=200;k++) dp[i][k] = min[idx[i][k]-1] + k*k;
            for(int k=1;k<=200;k++) min[i] = Math.min(min[i], dp[i][k]);
        }

        io.write(min[N] + "\n");

        io.close();

    }

}
```
