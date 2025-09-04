```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int INF = 70000;
    private static int[][] task;
    private static int[][] dp;
    private static int N, maxTime;

    public static void main(String[] args) throws IOException {
        init();
        DP();

        int answer = INF;
        for (int j = 0; j <= maxTime; j++) {
            if (dp[N][j] != INF) {
                answer = Math.min(answer, Math.max(j, dp[N][j]));
            }
        }

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        int a = 0;
        int b = 0;

        task = new int[2][N];

        for (int i = 0; i < N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            task[0][i] = Integer.parseInt(st.nextToken());
            task[1][i] = Integer.parseInt(st.nextToken());

            a += task[0][i];
            b += task[1][i];
        }

        maxTime = Math.max(a, b);

        dp = new int[N + 1][maxTime + 1];
        for (int i = 0; i <= N; i++) {
            Arrays.fill(dp[i], INF);
        }
        dp[0][0] = 0;
    }

    private static void DP() {
        for (int i = 0; i < N; i++) {
            for (int j = 0; j <= maxTime; j++) {
                if (dp[i][j] == INF) continue;

                if (j + task[0][i] <= maxTime) dp[i + 1][j + task[0][i]] = Math.min(dp[i + 1][j + task[0][i]], dp[i][j]);

                dp[i + 1][j] = Math.min(dp[i + 1][j], dp[i][j] + task[1][i]);
            }
        }
    }
}

```
