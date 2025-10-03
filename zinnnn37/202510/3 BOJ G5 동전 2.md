```java
package etc;

import java.io.*;
import java.util.Arrays;
import java.util.StringTokenizer;

public class BJ_2294_동전_2 {

	private static final int INF = 987654321;

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static       StringTokenizer st;

	private static int N, K;
	private static int[] coins, dp;

	public static void main(String[] args) throws IOException {
		init();
		sol();
	}

	private static void init() throws IOException {
		st = new StringTokenizer(br.readLine());
		N  = Integer.parseInt(st.nextToken());
		K  = Integer.parseInt(st.nextToken());

		coins = new int[N + 1];
		for (int i = 1; i <= N; i++) {
			coins[i] = Integer.parseInt(br.readLine());
		}

		dp = new int[K + 1];
		Arrays.fill(dp, INF);
		dp[0] = 0;
	}

	private static void sol() throws IOException {
		for (int i = 1; i <= K; i++) {
			for (int coin : coins) {
				if (i - coin >= 0 && dp[i - coin] != INF) {
					dp[i] = Math.min(dp[i], dp[i - coin] + 1);
				}
			}
		}
		bw.write(dp[K] != INF ? (dp[K] + "") : "-1");
		bw.flush();
		bw.close();
		br.close();
	}

}
```