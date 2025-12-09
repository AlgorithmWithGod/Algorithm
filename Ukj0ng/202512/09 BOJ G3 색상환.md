```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int INF = (int)1e9+3;
    private static int[][] dp;
    private static int N, K;

    public static void main(String[] args) throws IOException {
        init();
        DP();

        int answer = (dp[N-3][K-1] + dp[N-1][K]) % INF;
        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        K = Integer.parseInt(br.readLine());

        dp = new int[N][K+1];

        for (int i = 0; i < N; i++) {
            dp[i][0] = 1;
        }

        dp[1][1] = 1;
    }

    private static void DP() {
        for (int i = 2; i < N; i++) {
            for (int j = 1; j <= K; j++) {
                dp[i][j] = (dp[i-1][j] + dp[i-2][j-1]) % INF;
            }
        }
    }
}
```
