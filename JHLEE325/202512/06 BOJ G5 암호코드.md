```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String s = br.readLine();

        int n = s.length();
        int[] dp = new int[n + 1];
        int MOD = 1000000;

        if (s.charAt(0) == '0') {
            System.out.println(0);
            return;
        }

        dp[0] = 1;
        dp[1] = 1;

        for (int i = 2; i <= n; i++) {
            int one = s.charAt(i - 1) - '0';
            int two = (s.charAt(i - 2) - '0') * 10 + (s.charAt(i - 1) - '0');

            if (one >= 1 && one <= 9) {
                dp[i] = (dp[i] + dp[i - 1]) % MOD;
            }

            if (two >= 10 && two <= 26) {
                dp[i] = (dp[i] + dp[i - 2]) % MOD;
            }
        }

        System.out.println(dp[n]);
    }
}
```
