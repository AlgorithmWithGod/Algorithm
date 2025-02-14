```java
import java.util.*;
import java.io.*;

class Solution
{
	public static void main(String[] args) throws Exception{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        
        int N = Integer.parseInt(st.nextToken());
        int M = Integer.parseInt(st.nextToken());
        
        int[] boy = new int[N];
        int[] girl = new int[M];
        int[][] dp = new int[N+1][M+1];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
        	boy[i] = Integer.parseInt(st.nextToken());
        }
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < M; i++) {
        	girl[i] = Integer.parseInt(st.nextToken());
        }
        Arrays.sort(boy);
        Arrays.sort(girl);
        
        for (int i = 1; i <= N; i++) {
			for (int j = 1; j <= M; j++) {
				if(i == j) {
					dp[i][j] = dp[i-1][j-1] + Math.abs(boy[i-1]-girl[j-1]);
				}else if(i > j) {
					dp[i][j] = Math.min(dp[i-1][j-1] + Math.abs(boy[i-1]-girl[j-1]), dp[i-1][j]);
				}else if(i < j) {
					dp[i][j] = Math.min(dp[i-1][j-1] + Math.abs(boy[i-1]-girl[j-1]), dp[i][j-1]);					
				}
			}
		}
		System.out.println(dp[N][M]);
	}
}

```
