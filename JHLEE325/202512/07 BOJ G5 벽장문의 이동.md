```java
import java.io.*;
import java.util.*;

public class Main {

    static final int INF = 1_000_000_000;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int N = Integer.parseInt(br.readLine());

        st = new StringTokenizer(br.readLine());
        int open1 = Integer.parseInt(st.nextToken());
        int open2 = Integer.parseInt(st.nextToken());

        int K = Integer.parseInt(br.readLine());
        int[] use = new int[K + 1];
        for (int i = 1; i <= K; i++) {
            use[i] = Integer.parseInt(br.readLine());
        }

        int[][][] dp = new int[K + 1][N + 1][N + 1];
        for (int i = 0; i <= K; i++) {
            for (int a = 1; a <= N; a++) {
                Arrays.fill(dp[i][a], INF);
            }
        }

        dp[0][open1][open2] = 0;

        for (int i = 0; i < K; i++) {
            int x = use[i + 1];
            for (int a = 1; a <= N; a++) {
                for (int b = 1; b <= N; b++) {
                    if (dp[i][a][b] == INF) continue;

                    dp[i + 1][x][b] = Math.min(dp[i + 1][x][b], dp[i][a][b] + Math.abs(a - x));

                    dp[i + 1][a][x] = Math.min(dp[i + 1][a][x], dp[i][a][b] + Math.abs(b - x));
                }
            }
        }

        int answer = INF;
        for (int a = 1; a <= N; a++) {
            for (int b = 1; b <= N; b++) {
                answer = Math.min(answer, dp[K][a][b]);
            }
        }

        System.out.println(answer);
    }
}
```
