```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[][] map;
    private static int[][][] dp;
    private static int N, M;

    public static void main(String[] args) throws IOException {
        init();
        DP();

        bw.write(Math.max(dp[N][M][0], Math.max(dp[N][M][1], dp[N][M][2])) + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        map = new int[N+1][M+1];
        dp = new int[N+1][M+1][3];

        for (int i = 0; i <= N; i++) {
            for (int j = 0; j <= M; j++) {
                Arrays.fill(dp[i][j], Integer.MIN_VALUE / 2);
            }
        }

        for (int i = 1; i <= N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 1; j <= M; j++) {
                map[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        dp[1][1][0] = map[1][1];
        dp[1][1][1] = map[1][1];
        dp[1][1][2] = map[1][1];
    }

    private static void DP() {
        for (int i = 2; i <= M; i++) {
            dp[1][i][1] = dp[1][i-1][1] + map[1][i];
        }

        for (int i = 2; i <= N; i++) {
            for (int j = 1; j <= M; j++) {
                dp[i][j][0] = Math.max(dp[i-1][j][0], Math.max(dp[i-1][j][1], dp[i-1][j][2])) + map[i][j];
            }

            dp[i][1][1] = dp[i][1][0];
            for (int j = 2; j <= M; j++) {
                dp[i][j][1] = Math.max(dp[i][j][0], dp[i][j-1][1] + map[i][j]);
            }

            dp[i][M][2] = dp[i][M][0];
            for (int j = M-1; j >= 1; j--) {
                dp[i][j][2] = Math.max(dp[i][j][0], dp[i][j+1][2] + map[i][j]);
            }
        }
    }
}
```
