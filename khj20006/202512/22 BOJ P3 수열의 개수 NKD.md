```java
import java.util.*;
import java.io.*;

public class Main {

    static BufferedReader br;
    static BufferedWriter bw;
    static StringTokenizer st;

    static final long MOD = (long)1e9 + 7;
    static int N, K, D;
    static long[] dp;

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
        D = Integer.parseInt(st.nextToken());

        br.close();
    }

    public static void solve() throws Exception {
        bw = new BufferedWriter(new OutputStreamWriter(System.out));

        if(K > 446) {
            bw.write("0");
            return;
        }
        if(K == 1) {
            bw.write(N <= D ? "1" : "0");
            return;
        }

        dp = new long[N+2];
        for(int k=1;k<=K;k++) {
            long[] pre = new long[N+2];
            if(k == 1) {
                for(int i=1;i<=D;i++) {
                    if(2*i+1 <= N) pre[2*i+1] = (pre[2*i+1] + 1) % MOD;
                    if(2*i+D+1 <= N) pre[2*i+D+1] = (pre[2*i+D+1] + MOD - 1) % MOD;
                }
            }
            else {
                int limit = (long)k * D >= (long)N ? N : k * D;
                for(int i=1;i<=limit;i++) {
                    if(2*limit+1 <= N) pre[2*limit+1] = (pre[2*limit+1] + dp[i]) % MOD;
                    if(2*limit+D+1 <= N) pre[2*limit+D+1] = (pre[2*limit+D+1] + MOD - dp[i]) % MOD;
                }
            }

            long s = 0;
            for(int i=1;i<=N;i++) {
                s = (s + pre[i]) % MOD;
                pre[i] = s;
            }
            for(int i=1;i<=N;i++) dp[i] = pre[i];
        }
        bw.write(dp[N] + "\n");

        bw.close();
    }

}
```
