```java
import java.util.*;
import java.io.*;

class Solution
{
	public static void main(String[] args) throws Exception{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		
		int N = Integer.parseInt(st.nextToken());
		String target = br.readLine().trim();
		String reverseTarget = "";
		StringBuilder sb = new StringBuilder();
		int[][] dp = new int[N+1][N+1];
		for (int i = N-1; i > -1; i--) {
			sb.append(target.charAt(i));
		}
		reverseTarget = sb.toString();
		
		for (int i = 1; i < N+1; i++) {
			for (int j = 1; j < N+1; j++) {
				if (target.charAt(i-1) != reverseTarget.charAt(j-1)) {
					dp[i][j] = Math.max(dp[i][j-1], dp[i-1][j]);
				} else {
					dp[i][j] = dp[i-1][j-1] + 1;
				}
			}
		}
		
		System.out.println(N-dp[N][N]);
	}
}

```
