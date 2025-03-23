```java
import java.util.*;
import java.io.*;

class Solution
{
	public static void main(String[] args) throws Exception{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        
        int N = Integer.parseInt(st.nextToken());
        int[][] board = new int[N][3];
        int[][][] dp = new int[3][N][3];
        int answer = Integer.MAX_VALUE;
        
        for (int i = 0; i < N; i++) {
        	st = new StringTokenizer(br.readLine());
        	for (int j = 0; j < 3; j++) {
        		board[i][j] = Integer.parseInt(st.nextToken());
        	}
        }
        for (int k = 0; k < 3; k++) {
        	for (int i = 0; i < N; i++) {
        		Arrays.fill(dp[k][i], 1001);
        	}
        	for (int i = 0; i < N-1; i++) {
            	// 시작이 0일때
            	if (i == 0) {
            		dp[k][i][k] = board[0][k];
            		continue;
            	}
            	dp[k][i][0] = Math.min(dp[k][i-1][1], dp[k][i-1][2]) + board[i][0];
            	dp[k][i][1] = Math.min(dp[k][i-1][0], dp[k][i-1][2]) + board[i][1];
            	dp[k][i][2] = Math.min(dp[k][i-1][1], dp[k][i-1][0]) + board[i][2];
            }
        	if (k == 0) {
        		dp[k][N-1][1] = Math.min(dp[k][N-2][0], dp[k][N-2][2]) + board[N-1][1];
        		dp[k][N-1][2] = Math.min(dp[k][N-2][0], dp[k][N-2][1]) + board[N-1][2];
        		answer = Math.min(Math.min(dp[k][N-1][1], dp[k][N-1][2]), answer);
        	}
        	else if (k == 1) {
        		dp[k][N-1][0] = Math.min(dp[k][N-2][1], dp[k][N-2][2]) + board[N-1][0];
        		dp[k][N-1][2] = Math.min(dp[k][N-2][0], dp[k][N-2][1]) + board[N-1][2];
        		answer = Math.min(Math.min(dp[k][N-1][0], dp[k][N-1][2]), answer);
        	}
        	else if (k == 2) {
        		dp[k][N-1][1] = Math.min(dp[k][N-2][0], dp[k][N-2][2]) + board[N-1][1];
        		dp[k][N-1][0] = Math.min(dp[k][N-2][2], dp[k][N-2][1]) + board[N-1][0];
        		answer = Math.min(Math.min(dp[k][N-1][1], dp[k][N-1][0]), answer);
        	}
        }
        System.out.println(answer);
	}
}

```
