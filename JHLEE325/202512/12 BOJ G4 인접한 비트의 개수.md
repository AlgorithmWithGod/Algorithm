```java
import java.io.*;
import java.util.*;

public class Main {

    static long[][][] dp = new long[101][101][2];

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int T = Integer.parseInt(br.readLine());

        dp[1][0][0] = 1;
        dp[1][0][1] = 1;

        for (int n = 2; n <= 100; n++) {
            for (int k = 0; k <= 100; k++) {
                dp[n][k][0] = dp[n - 1][k][0] + dp[n - 1][k][1];

                dp[n][k][1] = dp[n - 1][k][0];
                if (k > 0) dp[n][k][1] += dp[n - 1][k - 1][1];
            }
        }

        StringBuilder sb = new StringBuilder();

        for (int t = 0; t < T; t++) {
            st = new StringTokenizer(br.readLine());
            int N = Integer.parseInt(st.nextToken());
            int K = Integer.parseInt(st.nextToken());

            sb.append(dp[N][K][0] + dp[N][K][1]).append("\n");
        }

        System.out.print(sb);
    }
}
```
