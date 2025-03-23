```java
import java.util.*;
import java.io.*;

public class Solution {
	public static void main(String[] args) throws Exception {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		
		int T = Integer.parseInt(st.nextToken());
		int[] N = new int[T];
		int maxN = 0;
		for (int tc = 0; tc < T; tc++) {
			st = new StringTokenizer(br.readLine());
			N[tc] = Integer.parseInt(st.nextToken());
			maxN = Math.max(maxN, N[tc]);
		}
		long[] dp = new long[maxN+1];
		dp[2] = 1;
		for (int i = 3; i <= maxN; i++) {
			long total = 1;
			long minus = 0;
			long divide = 1;
			for (int j = i; j > 2; j--) {
				total *= j;
				divide *= (i-j+1);
				minus += total*dp[j-1]/divide;
			}
			dp[i] = total*2 - (minus+1);
		}
		for (int i = 0; i < T; i++) {
			System.out.println(dp[N[i]]);
		}
	}
}
```
