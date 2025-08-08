```java
import java.io.*;
import java.util.*;

public class boj2229 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}

	public static void main(String[] args) throws Exception {
		nextLine();
		int N = nextInt();
		nextLine();
		int[] score = new int[N+1];
		int[] dp = new int[N+1];
		dp[0] = 0;
		int max = 0;
		for (int i = 1; i <= N; i++) {
			score[i] = nextInt();
			for (int j = i-1; j >= 1; j--) {
				max = Math.max(max, Math.abs(score[i] - score[j]) + dp[j-1]);
			}
			dp[i] = max;
		}
		System.out.println(dp[N]);
	}
}
```
