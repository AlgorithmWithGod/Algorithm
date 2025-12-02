```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int T = Integer.parseInt(st.nextToken());
        int W = Integer.parseInt(st.nextToken());

        int[] tree = new int[T + 1];
        for (int i = 1; i <= T; i++) {
            tree[i] = Integer.parseInt(br.readLine());
        }

        int[][][] dp = new int[T + 1][W + 1][3];

        for (int t = 1; t <= T; t++) {
            for (int w = 0; w <= W; w++) {

                if (w == 0) {
                    dp[t][0][1] = dp[t - 1][0][1] + (tree[t] == 1 ? 1 : 0);
                } else {
                    dp[t][w][1] = Math.max(dp[t - 1][w][1], dp[t - 1][w - 1][2]) + (tree[t] == 1 ? 1 : 0);
                    dp[t][w][2] = Math.max(dp[t - 1][w][2], dp[t - 1][w - 1][1]) + (tree[t] == 2 ? 1 : 0);
                }
            }
        }

        int answer = 0;
        for (int w = 0; w <= W; w++) {
            answer = Math.max(answer, dp[T][w][1]);
            answer = Math.max(answer, dp[T][w][2]);
        }

        System.out.println(answer);
    }
}
```
