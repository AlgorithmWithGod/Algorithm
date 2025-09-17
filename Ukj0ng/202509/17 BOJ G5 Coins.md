```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[] coins, dp;
    private static int N, M;

    public static void main(String[] args) throws IOException {
        int T = Integer.parseInt(br.readLine());

        while (T-->0) {
            init();
            DP();
            bw.write(dp[M] + "\n");
        }
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        StringTokenizer st = new StringTokenizer(br.readLine());
        coins = new int[N];
        for (int i = 0; i < N; i++) {
            coins[i] = Integer.parseInt(st.nextToken());
        }

        M = Integer.parseInt(br.readLine());
        dp = new int[M+1];

        dp[0] = 1;
    }

    private static void DP() {
        for (int i = 0; i < N; i++) {
            for (int j = 1; j <= M; j++) {
                if (j - coins[i] >= 0 && dp[j - coins[i]] > 0) {
                    dp[j] += dp[j - coins[i]];
                }
            }
        }
    }
}
```
