```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int T = Integer.parseInt(br.readLine());

        for (int t = 0; t < T; t++) {
            int K = Integer.parseInt(br.readLine());
            int[] files = new int[K + 1];
            int[] sum = new int[K + 1];
            int[][] dp = new int[K + 1][K + 1];

            StringTokenizer st = new StringTokenizer(br.readLine());
            for (int i = 1; i <= K; i++) {
                files[i] = Integer.parseInt(st.nextToken());
                sum[i] = sum[i - 1] + files[i];
            }

            for (int d = 1; d < K; d++) {
                for (int i = 1; i + d <= K; i++) {
                    int j = i + d;
                    dp[i][j] = Integer.MAX_VALUE;

                    for (int k = i; k < j; k++) {
                        dp[i][j] = Math.min(dp[i][j], dp[i][k] + dp[k + 1][j] + (sum[j] - sum[i - 1]));
                    }
                }
            }
            System.out.println(dp[1][K]);
        }
    }
}
```
