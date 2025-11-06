```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int MOD = 1000000000;
    private static int[][][] dp;
    private static int N;
    public static void main(String[] args) throws IOException {
        init();
        long answer = 0;
        for (int i = 0; i < 10; i++) {
            answer += dp[N][i][(1<<10) - 1];
            answer %= MOD;
        }

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        dp = new int[N+1][10][1<<10];

        for (int i = 1; i < 10; i++) {
            dp[1][i][1<<i] = 1;
        }

        for (int i = 2; i <= N; i++) {
            for (int j = 0; j < 10; j++) {
                for (int k = 0; k < 1<<10; k++) {
                    if (j < 9) {
                        dp[i][j+1][k | (1<<(j+1))] += dp[i-1][j][k];
                        dp[i][j+1][k | (1<<(j+1))] %= MOD;
                    }
                    if (j > 0) {
                        dp[i][j-1][k | (1<<(j-1))] += dp[i-1][j][k];
                        dp[i][j-1][k | (1<<(j-1))] %= MOD;
                    }
                }
            }
        }
    }
}
```
