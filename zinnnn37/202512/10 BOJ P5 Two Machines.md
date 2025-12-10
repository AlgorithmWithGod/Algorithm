```java
import java.io.*;
import java.util.Arrays;
import java.util.StringTokenizer;

public class BJ_17628_Two_Machines {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int N, totalA, ans;
    private static int[][] works, dp;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        totalA = 0;
        ans = Integer.MAX_VALUE;

        works = new int[N + 1][2];
        for (int i = 1; i <= N; i++) {
            st = new StringTokenizer(br.readLine());

            works[i][0] = Integer.parseInt(st.nextToken());
            works[i][1] = Integer.parseInt(st.nextToken());

            totalA += works[i][0];
        }
        // A의 시간을 j로 만들 때, B의 최소 시간
        dp = new int[N + 1][totalA + 1];
        for (int[] row : dp) {
            Arrays.fill(row, Integer.MAX_VALUE);
        }
        dp[0][0] = 0;
    }

    private static void sol() throws IOException {
        for (int i = 1; i <= N; i++) {
            for (int j = 0; j <= totalA; j++) {
                if (dp[i - 1][j] == Integer.MAX_VALUE) {
                    continue;
                }
                dp[i][j] = Math.min(dp[i][j], dp[i - 1][j] + works[i][1]);

                if (j + works[i][0] <= totalA) {
                    dp[i][j + works[i][0]] = Math.min(dp[i][j + works[i][0]], dp[i - 1][j]);
                }
            }
        }

        for (int j = 0; j <= totalA; j++) {
            if (dp[N][j] == Integer.MAX_VALUE) {
                continue;
            }
            ans = Math.min(ans, Math.max(j, dp[N][j]));
        }
        bw.write(ans + "");
        bw.flush();
        bw.close();
        br.close();
    }

}
```