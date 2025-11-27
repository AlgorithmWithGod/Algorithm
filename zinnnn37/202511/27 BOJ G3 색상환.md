```java
import java.io.*;

public class BJ_G3_색상환 {

    private static final int MOD = 1_000_000_003;

    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

    private static int N, K;
    private static int[][] dp;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        K = Integer.parseInt(br.readLine());

        dp = new int[N + 1][K + 1];
        for (int i = 0; i <= N; i++) {
            dp[i][0] = 1;
            if (i >= 1) dp[i][1] = i;
        }
    }

    private static void sol() throws IOException {
        for (int i = 4; i <= N; i++) {
            for (int j = 2; j <= K; j++) {
                dp[i][j] = (dp[i - 1][j] + dp[i - 2][j - 1]) % MOD;
            }
        }

        bw.write(dp[N][K] + "");
        bw.flush();
        bw.close();
        br.close();
    }

}
```