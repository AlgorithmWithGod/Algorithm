```java
import java.io.*;
import java.util.Arrays;
import java.util.StringTokenizer;

public class BJ_17404_RGB거리_2 {

    private static final int INF = 987654321;

    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static StringTokenizer st;

    private static int N, ans;
    private static int[][] colors;
    private static int[][] dp;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        ans = INF;

        colors = new int[N][3];
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < 3; j++) {
                colors[i][j] = Integer.parseInt(st.nextToken());
            }
        }
        dp = new int[N][3];
    }

    private static void sol() throws IOException {
        // 시작 색 지정
        for (int firstColor = 0; firstColor < 3; firstColor++) {
            Arrays.fill(dp[0], INF);

            dp[0][firstColor] = colors[0][firstColor];

            for (int i = 1; i < N; i++) {
                dp[i][0] = Math.min(dp[i - 1][1], dp[i - 1][2]) + colors[i][0];
                dp[i][1] = Math.min(dp[i - 1][0], dp[i - 1][2]) + colors[i][1];
                dp[i][2] = Math.min(dp[i - 1][0], dp[i - 1][1]) + colors[i][2];
            }

            for (int lastColor = 0; lastColor < 3; lastColor++) {
                if (lastColor != firstColor) {
                    ans = Math.min(ans, dp[N - 1][lastColor]);
                }
            }
        }
        bw.write(ans + "");
        bw.flush();
        bw.close();
        br.close();
    }

}
```