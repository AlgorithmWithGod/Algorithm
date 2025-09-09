```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[][] dp;
    private static int[] file, sum;
    private static int K;

    public static void main(String[] args) throws IOException {
        int T = Integer.parseInt(br.readLine());
        while (T-- > 0) {
            init();
            DP();
            bw.write(dp[1][K] + "\n");
        }
        bw.flush();
        bw.close();
        br.close();

    }

    private static void init() throws IOException {
        K = Integer.parseInt(br.readLine());
        StringTokenizer st = new StringTokenizer(br.readLine());

        file = new int[K+1];
        sum = new int[K+1];
        dp = new int[K+1][K+1];

        for (int i = 1; i <= K; i++) {
            file[i] = Integer.parseInt(st.nextToken());
            sum[i] = sum[i-1] + file[i];
        }
    }

    private static void DP() {
        for (int i = 2; i <= K; i++) {
            for (int j = 1; j <= K-i+1; j++) {
                int k = i+j-1;
                dp[j][k] = Integer.MAX_VALUE;

                for (int l = j; l < k; l++) {
                    int cost = dp[j][l] + dp[l+1][k] + sum[k] - sum[j-1];
                    dp[j][k] = Math.min(cost, dp[j][k]);
                }
            }
        }
    }
}
```
