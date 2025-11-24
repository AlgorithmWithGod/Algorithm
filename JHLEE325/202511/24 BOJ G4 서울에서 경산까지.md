```java
import java.io.*;
import java.util.*;

public class Main {
    static final int INF = -987654321;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int N = Integer.parseInt(st.nextToken());
        int T = Integer.parseInt(st.nextToken());

        int[] walk = new int[N];
        int[] walkMoney = new int[N];
        int[] bike = new int[N];
        int[] bikeMoney = new int[N];

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            walk[i] = Integer.parseInt(st.nextToken());
            walkMoney[i] = Integer.parseInt(st.nextToken());
            bike[i] = Integer.parseInt(st.nextToken());
            bikeMoney[i] = Integer.parseInt(st.nextToken());
        }

        int[][] dp = new int[N + 1][T + 1];
        for (int[] row : dp) Arrays.fill(row, INF);
        dp[0][0] = 0;

        for (int i = 0; i < N; i++) {
            for (int t = 0; t <= T; t++) {
                if (dp[i][t] == INF) continue;

                if (t + walk[i] <= T) {
                    dp[i + 1][t + walk[i]] = Math.max(dp[i + 1][t + walk[i]], dp[i][t] + walkMoney[i]);
                }

                if (t + bike[i] <= T) {
                    dp[i + 1][t + bike[i]] = Math.max(dp[i + 1][t + bike[i]], dp[i][t] + bikeMoney[i]);
                }
            }
        }

        int res = 0;
        for (int t = 0; t <= T; t++) {
            res = Math.max(res, dp[N][t]);
        }

        System.out.println(res);
    }
}
```
