```java
class Solution {
    private static final int MOD = 1234567;
    private int[] memo;
    
    public int solution(int n) {
        memo = new int[n + 1];
        return fib(n);
    }
    
    private int fib(int n) {
        if (n == 0) return 0;
        if (n == 1) return 1;
        
        // 이미 계산된 값이 있으면 반환
        if (memo[n] != 0) {
            return memo[n];
        }
        
        // 계산 후 메모에 저장
        memo[n] = (fib(n - 1) + fib(n - 2)) % MOD;
        return memo[n];
    }
}
```
