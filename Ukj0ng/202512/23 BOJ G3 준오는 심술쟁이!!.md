```
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int MOD = (int) 1e9+7;
    private static int[][] dp;
    private static int s;
    private static String str;

    public static void main(String[] args) throws IOException {
        init();
        DP();

        bw.write(dp[str.length()][s] + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        s = Integer.parseInt(br.readLine());
        str = br.readLine();

        dp = new int[str.length()+1][s+1];

        dp[0][0] = 1;
        for (int i = 1; i <= str.length(); i++) {
            dp[i][0] = 1;
        }
        for (int i = 1; i <= s && i <= 25; i++) {
            dp[1][i] = 1;
        }
    }

    private static void DP() {
        for (int i = 2; i <= str.length(); i++) {
            for (int j = 1; j <= s; j++) {
                if (j >= 26) {
                    int val = (dp[i][j-1] + dp[i-1][j]) % MOD;
                    dp[i][j] = (val - dp[i-1][j-26] + MOD) % MOD;
                } else {
                    dp[i][j] = (dp[i][j-1] + dp[i-1][j]) % MOD;
                }
            }
        }
    }
}
```
