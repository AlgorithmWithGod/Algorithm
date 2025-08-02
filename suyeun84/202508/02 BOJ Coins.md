```java
import java.io.*;
import java.util.*;

public class boj3067 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}

	public static void main(String[] args) throws Exception {
		nextLine();
		int T = nextInt();
		for (int tc = 1; tc <= T; tc++) {
			nextLine();
			int N = nextInt();
			int[] coins = new int[N+1];
			nextLine();
			for (int i = 1; i <= N; i++) coins[i] = nextInt();
			nextLine();
			int M = nextInt();
			int[][] dp = new int[N+1][M+1];
			for (int i = 1; i <= N; i++) {
				dp[i][0] = 1;
				for (int j = 1; j <= M; j++) {
					dp[i][j] = dp[i-1][j];
					if (j >= coins[i]) dp[i][j] += dp[i][j-coins[i]];
				}
			}
			System.out.println(dp[N][M]);
		}
	}
}
```
