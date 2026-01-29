```java
import java.util.*;
import java.io.*;

public class Main {
    
    static int MOD = 1000000;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());

        int[][][] dp = new int[N + 1][2][3];

        dp[0][0][0] = 1;

        for (int i = 0; i < N; i++) {
            for (int j = 0; j < 2; j++) {
                for (int k = 0; k < 3; k++) {
                    if (dp[i][j][k] == 0) continue;

                    dp[i + 1][j][0] = (dp[i + 1][j][0] + dp[i][j][k]) % MOD;

                    if (j + 1 < 2) {
                        dp[i + 1][j + 1][0] = (dp[i + 1][j + 1][0] + dp[i][j][k]) % MOD;
                    }

                    if (k + 1 < 3) {
                        dp[i + 1][j][k + 1] = (dp[i + 1][j][k + 1] + dp[i][j][k]) % MOD;
                    }
                }
            }
        }

        int ans = 0;
        for (int j = 0; j < 2; j++) {
            for (int k = 0; k < 3; k++) {
                ans = (ans + dp[N][j][k]) % MOD;
            }
        }

        System.out.println(ans);
    }
}
```
