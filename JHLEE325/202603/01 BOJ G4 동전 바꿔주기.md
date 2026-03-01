```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int T = Integer.parseInt(br.readLine());
        int k = Integer.parseInt(br.readLine());

        int[] dp = new int[T + 1];
        dp[0] = 1;

        for (int i = 0; i < k; i++) {
            st = new StringTokenizer(br.readLine());
            int p = Integer.parseInt(st.nextToken());
            int n = Integer.parseInt(st.nextToken());

            for (int m = T; m >= 1; m--) {
                for (int c = 1; c <= n; c++) {
                    int budget = p * c;

                    if (m - budget >= 0) {
                        dp[m] += dp[m - budget];
                    } else {
                        break;
                    }
                }
            }
        }

        System.out.println(dp[T]);
    }
}
```
