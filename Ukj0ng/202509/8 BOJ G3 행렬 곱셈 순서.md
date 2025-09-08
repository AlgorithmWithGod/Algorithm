```
import java.io.*;
        import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[][] matrix, dp;
    private static int N;

    public static void main(String[] args) throws IOException {
        init();
        DP();

        bw.write(dp[1][N] + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        matrix = new int[N+1][2];
        dp = new int[N+1][N+1];

        for (int i = 1; i <= N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            matrix[i][0] = Integer.parseInt(st.nextToken());
            matrix[i][1] = Integer.parseInt(st.nextToken());
        }
    }

    private static void DP() {
        for (int i = 1; i < N; i++) {
            dp[i][i+1] = matrix[i][0] * matrix[i][1] * matrix[i+1][1];
        }

        for (int len = 2; len <= N; len++) {
            for (int start = 1; start <= N - len + 1; start++) {
                int end = start + len - 1;
                dp[start][end] = Integer.MAX_VALUE;

                for (int k = start; k < end; k++) {
                    int cost = dp[start][k] + dp[k+1][end]
                            + matrix[start][0] * matrix[k][1] * matrix[end][1];
                    dp[start][end] = Math.min(dp[start][end], cost);
                }
            }
        }
    }
}
```
