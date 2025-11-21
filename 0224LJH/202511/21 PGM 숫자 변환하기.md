```java
import java.io.*;
import java.util.*;

class Solution {
    public int solution(int x, int y, int n) {
        int[] dp = new int[1_000_001];
        Arrays.fill(dp,Integer.MAX_VALUE/2);
        dp[x] = 0;
        
        for (int i = x; i <= y; i++){
            if (dp[i] >= Integer.MAX_VALUE/2) continue;
            int next = i+n;
            int mul2 = i*2;
            int mul3 = i*3;
            
            if ( next <= 1000_000){
                dp[next] = Math.min(dp[i]+1,dp[next]);
            }
            if ( mul2 <= 1000_000){
                dp[mul2] = Math.min(dp[i]+1,dp[mul2]);
            }
            if ( mul3 <= 1000_000){
                dp[mul3] = Math.min(dp[i]+1,dp[mul3]);
            }
        }
        
        
        
        int answer = (dp[y]!=Integer.MAX_VALUE/2?dp[y]:-1);
        return answer;
    }
}
```
