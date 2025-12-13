```java
import java.io.*;
import java.util.Arrays;
import java.util.StringTokenizer;

public class BJ_2169_로봇_조종하기 {
    private static final int INF = -987654321;

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int N, M;
    private static int[] ldp, rdp;
    private static int[][] matrix, dp;

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
        ldp = new int[M + 2];
        rdp = new int[M + 2];

        for (int i = 2; i <= N; i++) {
            Arrays.fill(dp[i], INF);
        }

        for (int i = 1; i <= M; i++) {
            dp[1][i] = dp[1][i - 1] + matrix[1][i];
        }
    }

    private static void sol() throws IOException {
        for (int i = 2; i <= N; i++) {
            clear();
            for (int j = 1; j <= M; j++) {
                ldp[j] = matrix[i][j] + Math.max(dp[i - 1][j], ldp[j - 1]);
            }

            for (int j = M; j > 0; j--) {
                rdp[j] = matrix[i][j] + Math.max(dp[i - 1][j], rdp[j + 1]);
            }

            for (int j = 1; j <= M; j++) {
                dp[i][j] = Math.max(ldp[j], rdp[j]);
            }
        }

        bw.write(dp[N][M] + "");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void clear() {
        Arrays.fill(ldp, INF);
        Arrays.fill(rdp, INF);
    }

}
```