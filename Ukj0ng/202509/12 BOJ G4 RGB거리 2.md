```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int INF = 1000010;
    private static int[][] cost, dp;
    private static int N;

    public static void main(String[] args) throws IOException {
        init();

        int answer = Integer.MAX_VALUE;
        for (int i = 0; i < 3; i++) {
            DP(i);

            for (int j = 0; j < 3; j++) {
                answer = Math.min(answer, dp[N-1][j]);
            }
        }

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();

    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        cost = new int[N][3];
        dp = new int[N][3];

        for (int i = 0; i < N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            for (int j = 0; j < 3; j++) {
                cost[i][j] = Integer.parseInt(st.nextToken());
            }
        }
    }

    private static void DP(int start) {
        for (int i = 0; i < N; i++) Arrays.fill(dp[i], INF);

        dp[0][start] = cost[0][start];

        for (int i = 1; i < N-1; i++) {
            dp[i][0] = cost[i][0] + Math.min(dp[i-1][1], dp[i-1][2]);
            dp[i][1] = cost[i][1] + Math.min(dp[i-1][0], dp[i-1][2]);
            dp[i][2] = cost[i][2] + Math.min(dp[i-1][0], dp[i-1][1]);
        }

        for (int i = 0; i < 3; i++) {
            if (i == start) continue;

            int min = INF;

            for (int j = 0; j < 3; j++) {
                if (i == j) continue;
                min = Math.min(min, dp[N-2][j]);
            }

            dp[N-1][i] = cost[N-1][i] + min;
        }
    }
}
```
