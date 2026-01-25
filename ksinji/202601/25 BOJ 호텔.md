```java
import java.io.*;
import java.util.*;

public class Main {
    static int c, n;
    static int[] dp;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        c = Integer.parseInt(st.nextToken());
        n = Integer.parseInt(st.nextToken());

        int max = c + 100;
        dp = new int[max + 1];

        Arrays.fill(dp, Integer.MAX_VALUE);
        dp[0] = 0;

        for (int i = 0; i < n; i++) {
            st = new StringTokenizer(br.readLine());
            int cost = Integer.parseInt(st.nextToken());
            int gain = Integer.parseInt(st.nextToken());

            for (int j = gain; j <= max; j++) {
                if (dp[j - gain] == Integer.MAX_VALUE) {
                    continue;
                }
                dp[j] = Math.min(dp[j], dp[j - gain] + cost);
            }
        }

        int ans = Integer.MAX_VALUE;
        for (int i = c; i <= max; i++) {
            ans = Math.min(ans, dp[i]);
        }

        System.out.println(ans);
    }
}
```
