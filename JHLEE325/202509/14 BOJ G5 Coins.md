```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        StringBuilder sb = new StringBuilder();

        int T = Integer.parseInt(br.readLine());

        for (int t = 0; t < T; t++) {
            int n = Integer.parseInt(br.readLine());
            int[] arr = new int[n];

            st = new StringTokenizer(br.readLine());
            for (int i = 0; i < n; i++) {
                arr[i] = Integer.parseInt(st.nextToken());
            }

            int m = Integer.parseInt(br.readLine());
            int[] dp = new int[m + 1];
            dp[0] = 1;

            for (int i = 0; i < n; i++) {
                int coin = arr[i];
                for (int j = coin; j <= m; j++) {
                    dp[j] += dp[j - coin];
                }
            }

            sb.append(dp[m]).append("\n");
        }

        System.out.print(sb);
    }
}

```
