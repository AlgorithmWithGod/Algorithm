```java
import java.util.*;

public class Main {
    static final int MOD = 1000000003;
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();
        int K = sc.nextInt();
        
        if (K * 2 > N) {
            System.out.println(0);
            return;
        }
        
        if (K == 1) {
            System.out.println(N);
            return;
        }

        long case1 = solve(N - 3, K - 1);
        long case2 = solve(N - 1, K);
        
        long answer = (case1 + case2) % MOD;
        System.out.println(answer);
    }
    
    static long solve(int n, int k) {
        if (n < 0 || k < 0) return 0;
        if (k == 0) return 1;
        if (n < k) return 0;
        if (k * 2 - 1 > n) return 0;
        
        long[][] dp = new long[n + 1][k + 1];
        
        dp[0][0] = 1;
        if (n >= 1) {
            dp[1][0] = 1;
            dp[1][1] = 1;
        }
        
        for (int i = 2; i <= n; i++) {
            dp[i][0] = 1;
            for (int j = 1; j <= Math.min(i, k); j++) {
                dp[i][j] = (dp[i - 1][j] + dp[i - 2][j - 1]) % MOD;
            }
        }
        
        return dp[n][k];
    }
}
```
