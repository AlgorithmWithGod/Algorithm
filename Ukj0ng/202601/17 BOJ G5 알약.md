```
import java.io.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static long[][] dp;
    private static int N;

    public static void main(String[] args) throws IOException {
        init();

        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        while (true) {
            N = Integer.parseInt(br.readLine());
            if (N == 0) return;

            dp = new long[N+1][N+1];

            for (int i = 0; i <= N; i++) {
                dp[0][i] = 1;
            }

            for (int i = 1; i <= N; i++) {
                for (int j = 0; j <= N; j++) {

                    if (j+1 <= N)dp[i][j] += dp[i-1][j+1];

                    if (j > 0) dp[i][j] += dp[i][j-1];
                }
            }

            bw.write(dp[N][0] + "\n");
        }
    }
}
```
