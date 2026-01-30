```java
import java.io.*;
import java.util.*;

public class Main {

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int N = Integer.parseInt(br.readLine());

        int[] train = new int[N + 1];
        int[] sum = new int[N + 1];

        st = new StringTokenizer(br.readLine());
        for (int i = 1; i <= N; i++) {
            train[i] = Integer.parseInt(st.nextToken());
            sum[i] = sum[i - 1] + train[i];
        }

        int K = Integer.parseInt(br.readLine());

        int[][] dp = new int[4][N + 1];

        for (int i = 1; i <= 3; i++) {
            for (int j = i * K; j <= N; j++) {
                dp[i][j] = Math.max(dp[i][j - 1], dp[i - 1][j - K] + (sum[j] - sum[j - K]));
            }
        }

        System.out.println(dp[3][N]);
    }
}
```
