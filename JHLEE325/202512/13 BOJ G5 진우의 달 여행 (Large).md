```java
import java.io.*;
import java.util.*;

public class Main {

    static final int INF = 1_000_000_000;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int N = Integer.parseInt(st.nextToken());
        int M = Integer.parseInt(st.nextToken());

        int[][] cost = new int[N][M];
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < M; j++) {
                cost[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        int[][][] dp = new int[N][M][3];

        for (int j = 0; j < M; j++) {
            for (int d = 0; d < 3; d++) {
                dp[0][j][d] = cost[0][j];
            }
        }

        for (int i = 1; i < N; i++) {
            for (int j = 0; j < M; j++) {
                Arrays.fill(dp[i][j], INF);

                if (j + 1 < M) {
                    dp[i][j][0] = Math.min(dp[i - 1][j + 1][1], dp[i - 1][j + 1][2]) + cost[i][j];
                }

                dp[i][j][1] = Math.min(dp[i - 1][j][0], dp[i - 1][j][2]) + cost[i][j];

                if (j - 1 >= 0) {
                    dp[i][j][2] = Math.min(dp[i - 1][j - 1][0], dp[i - 1][j - 1][1]) + cost[i][j];
                }
            }
        }

        int answer = INF;
        for (int j = 0; j < M; j++) {
            for (int d = 0; d < 3; d++) {
                answer = Math.min(answer, dp[N - 1][j][d]);
            }
        }

        System.out.println(answer);
    }
}
```
