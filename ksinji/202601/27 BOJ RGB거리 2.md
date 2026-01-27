```java
import java.io.*;
import java.util.*;

public class Main {
    static int n;
    static int[][] cost;
    static int[][] dp;

    static final int INF = 1_000_000_000;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        n = Integer.parseInt(br.readLine());
        cost = new int[n][3];

        for (int i = 0; i < n; i++) {
            st = new StringTokenizer(br.readLine());
            cost[i][0] = Integer.parseInt(st.nextToken());
            cost[i][1] = Integer.parseInt(st.nextToken());
            cost[i][2] = Integer.parseInt(st.nextToken());
        }

        int ans = INF;

        for (int firstColor = 0; firstColor < 3; firstColor++) {
            dp = new int[n][3];

            for (int c = 0; c < 3; c++) {
                if (c == firstColor) {
                    dp[0][c] = cost[0][c];
                } else {
                    dp[0][c] = INF;
                }
            }

            for (int i = 1; i < n; i++) {
                dp[i][0] = Math.min(dp[i - 1][1], dp[i - 1][2]) + cost[i][0];
                dp[i][1] = Math.min(dp[i - 1][0], dp[i - 1][2]) + cost[i][1];
                dp[i][2] = Math.min(dp[i - 1][0], dp[i - 1][1]) + cost[i][2];
            }

            for (int lastColor = 0; lastColor < 3; lastColor++) {
                if (lastColor != firstColor) {
                    ans = Math.min(ans, dp[n - 1][lastColor]);
                }
            }
        }

        System.out.println(ans);
```
    }
}
