```java
import java.io.*;
import java.util.Arrays;
import java.util.StringTokenizer;

public class BJ_26259_백룸 {

    private static final int             INF = -987654321;
    private static final BufferedReader  br  = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw  = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int N, M;
    private static boolean isHorizontal;
    private static int[][] matrix, dp;
    private static boolean[][] wall;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        matrix = new int[N + 1][M + 1];
        for (int i = 1; i <= N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 1; j <= M; j++) {
                matrix[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        dp = new int[N + 1][M + 1];
        for (int[] d : dp) Arrays.fill(d, INF);
        dp[1][1] = matrix[1][1];

        wall = new boolean[N + 1][M + 1];
        st = new StringTokenizer(br.readLine());
        int x1 = Integer.parseInt(st.nextToken());
        int y1 = Integer.parseInt(st.nextToken());
        int x2 = Integer.parseInt(st.nextToken());
        int y2 = Integer.parseInt(st.nextToken());

        if (x1 == x2 && y1 == y2) return;

        isHorizontal = (x1 == x2);

        if (isHorizontal && x1 < N) {
            int start = Math.min(y1, y2) + 1;
            int end   = Math.max(y1, y2);
            for (int y = start; y <= end; y++) {
                wall[x1 + 1][y] = true;
            }
        } else if (!isHorizontal && y1 < M) {
            int start = Math.min(x1, x2) + 1;
            int end   = Math.max(x1, x2);
            for (int x = start; x <= end; x++) {
                wall[x][y1 + 1] = true;
            }
        }
    }

    private static void sol() throws IOException {
        for (int i = 1; i <= N; i++) {
            for (int j = 1; j <= M; j++) {
                if (i == 1 && j == 1) continue;

                if (wall[i][j]) {
                    if (isHorizontal && dp[i][j - 1] != INF) {
                        dp[i][j] = matrix[i][j] + dp[i][j - 1];
                    } else if (!isHorizontal && dp[i - 1][j] != INF) {
                        dp[i][j] = matrix[i][j] + dp[i - 1][j];
                    }
                } else {
                    int up   = dp[i - 1][j];
                    int left = dp[i][j - 1];
                    if (up != INF || left != INF) {
                        dp[i][j] = matrix[i][j] + Math.max(up, left);
                    }
                }
            }
        }

        bw.write(dp[N][M] == INF ? "Entity" : String.valueOf(dp[N][M]));
        bw.flush();
        bw.close();
        br.close();
    }

}
```