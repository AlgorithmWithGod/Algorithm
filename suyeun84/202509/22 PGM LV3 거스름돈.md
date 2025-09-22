```java
class Solution {
    public int solution(int n, int[] money) {
        int answer = 0;
        final int MOD = 1000000007;
        int[][] dp = new int[money.length + 1][n + 1];
        
        for (int i = 1; i < money.length+1; i++) {
            for (int j = 0; j <= n; j++) {
                if (j == 0) {
                    dp[i][j] = 1;
                } else if (j - money[i-1] >= 0) {
                    dp[i][j] = (dp[i - 1][j] + dp[i][j - money[i - 1]]) % MOD;
                } else
                    dp[i][j] = dp[i - 1][j];
            }
        }

        return dp[money.length][n];
    }
}
```
