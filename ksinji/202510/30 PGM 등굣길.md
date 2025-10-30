```java
class Solution {
    static final int MOD = 1000000007;
    public int solution(int m, int n, int[][] puddles) {
        int[][] dp = new int[n+1][m+1];
        
        dp[1][1] = 1;
        
        for (int[] p: puddles){
            dp[p[1]][p[0]] = -1;
        }
        
        for (int i=1; i<n+1; i++){
            for (int j=1; j<m+1; j++){
                if (i==1 && j==1){
                    continue;
                }
                
                if (dp[i][j] == -1) {
                    continue;
                } else if (dp[i-1][j] == -1) {
                    dp[i][j] = dp[i][j-1]%MOD;
                } else if (dp[i][j-1] == -1) {
                    dp[i][j] = dp[i-1][j]%MOD;
                } else {
                    dp[i][j] = (dp[i][j-1]+dp[i-1][j])%MOD;
                }
            }
        }
        
        return dp[n][m];
    }
}
```
