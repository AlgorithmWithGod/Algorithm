```java
import java.io.*;

public class BJ_4384_공평하게_팀_나누기 {

    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

    private static int N, sum;
    private static int[] weight;
    private static boolean[][] dp;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        sum = 0;

        weight = new int[N];
        for (int i = 0; i < N; i++) {
            weight[i] = Integer.parseInt(br.readLine());
            sum += weight[i];
        }

        dp = new boolean[N / 2 + 1][sum + 1];
        dp[0][0] = true;
    }

    private static void sol() throws IOException {
        // 각 사람에 대해
        for (int k = 0; k < N; k++) {
            for (int i = N / 2; i > 0; i--) {
                for (int j = sum; j >= weight[k]; j--) {
                    if (dp[i - 1][j - weight[k]]) {
                        dp[i][j] = true;
                    }
                }
            }
        }

        int minDiff = Integer.MAX_VALUE;
        int ans = 0;
        for (int j = 0; j <= sum; j++) {
            if (dp[N / 2][j]) {
                int diff = Math.abs(sum - j - j);
                if (minDiff > diff) {
                    minDiff = diff;
                    ans = j;
                }
            }
        }
        bw.write(Math.min(ans, sum - ans) + " " + Math.max(ans, sum - ans));
        bw.flush();
        bw.close();
        br.close();
    }

}
```