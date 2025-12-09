```java
import java.io.*;

public class Main {
    static final int MOD = 1000000;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String s = br.readLine();

        int n = s.length();
        if (n == 0 || s.charAt(0) == '0') {
            System.out.println(0);
            return;
        }

        int[] dp = new int[n + 1];
        dp[0] = 1;
        dp[1] = 1;

        for (int i = 2; i <= n; i++) {
            char c1 = s.charAt(i - 1);
            char c0 = s.charAt(i - 2);

            if (c1 != '0') {
                dp[i] += dp[i - 1];
                dp[i] %= MOD;
            }

            int two = (c0 - '0') * 10 + (c1 - '0');
            if (two >= 10 && two <= 26) {
                dp[i] += dp[i - 2];
                dp[i] %= MOD;
            }
        }

        System.out.println(dp[n] % MOD);
    }
}

```
