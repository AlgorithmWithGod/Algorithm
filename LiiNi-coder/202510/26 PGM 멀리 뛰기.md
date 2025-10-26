```java
class Solution {
    private static long[] dp;
    public long solution(int n) {
        dp = new long[n + 1];
        dp[1] = 1;
        if (n >= 2)
          dp[2] = 2;
        return getDp(n);
    }

    private long getDp(int n) {
        if (dp[n] != 0) return dp[n];
        dp[n] = (getDp(n - 1) + getDp(n - 2)) % 1234567;
        return dp[n];
    }
}

```
