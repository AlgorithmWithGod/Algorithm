```java
import java.io.*;
import java.util.*;

class Solution {
    static int size;
    static boolean[] hasTop;
    static int[][] dp;
    
    static final int EMPTY = 0;
    static final int LEFT = 1;
    static final int TOP = 2;
    static final int RIGHT = 3;
    static final int REMAINDER = 10007;
    
    public int solution(int n, int[] tops) {
        size = n;
        hasTop = new boolean[n];
        dp = new int[size][4];

        for (int i = 0; i < n; i++) hasTop[i] = tops[i] == 1;
        
        process();
        
        
        int answer = dp[size-1][EMPTY] + dp[size-1][LEFT] +  dp[size-1][TOP] +  dp[size-1][RIGHT] ;
        answer %= REMAINDER;
        return answer;
    }
    
    private void process(){
        // i번칸의 경우의 수
        // dp[i][아무것도 안함]=  dp[i-1][모든 경우]
        // dp[i][왼쪽으로 뻗음] = dp[i-1][왼쪽으로 뻗음] + dp[i-1][위로뻗음] + dp[i-1][아무것도 안함]
        // dp[i][위로 뻗음] = (top이 있음)? dp[i-1][모든 경우]: 0;
        // dp[i][오른쪽으로 뻗음] = dp[i-1]모든 경우
        
        dp[0][EMPTY] = 1;
        dp[0][LEFT] = 1;
        dp[0][RIGHT] = 1;
        if (hasTop[0]) dp[0][TOP] = 1;
        
        for (int i = 1; i < size; i++){
            int sum = dp[i-1][EMPTY] + dp[i-1][TOP] + dp[i-1][LEFT] + dp[i-1][RIGHT];
            dp[i][EMPTY] = sum%REMAINDER;
            dp[i][LEFT] = (sum-dp[i-1][RIGHT])%REMAINDER;
            dp[i][RIGHT] = sum%REMAINDER;
            if(hasTop[i]) dp[i][TOP] = sum%REMAINDER;
        }
    }
}
```
