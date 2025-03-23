```java
import java.util.*;

public class Main {
    final static int MOD = 1_000_000_003;
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int N = sc.nextInt();
        int K = sc.nextInt();
        
        // dp[i][j] = i번째 색상까지 고려하여 j개를 뽑는 경우의 수
        int[][] dp = new int[N+1][K+1];
        for (int i = 1; i < N+1; i++) {
            dp[i][0] = 1;
            dp[i][1] = i;
        }
        for (int i = 3; i < N; i++) {
            for (int j = 2; j < K+1; j++) {
                dp[i][j] = (dp[i-1][j] + dp[i-2][j-1]) % MOD;
            }
        }
        // 마지막 색상 처리
        // dp[N - 2- 1][K-1] = 1번 색상을 제외하고 N-2 색상까지 K-1개의 색을 겹치지 않게 칠하는 경우
        dp[N][K] = (dp[N - 2 - 1][K-1] + dp[N-1][K]) % MOD;
        
        int answer = dp[N][K];
        System.out.println(answer);

        sc.close();
    }
}
```
