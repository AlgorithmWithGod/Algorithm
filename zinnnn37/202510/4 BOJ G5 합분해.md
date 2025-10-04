```java
import java.io.*;
import java.util.Arrays;
import java.util.StringTokenizer;

public class BJ_2225_합분해 {

	private static final int MOD = 1_000_000_000;

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static       StringTokenizer st;

	private static int N, K;
	private static int[] dp;

	public static void main(String[] args) throws IOException {
		init();
		sol();
	}

	private static void init() throws IOException {
		st = new StringTokenizer(br.readLine());
		N  = Integer.parseInt(st.nextToken());
		K  = Integer.parseInt(st.nextToken());

		dp = new int[N + 1];
		Arrays.fill(dp, 1);
	}

	private static void sol() throws IOException {
		for (int j = 1; j < K; j++) {
			for (int i = 1; i <= N; i++) {
				dp[i] = (dp[i - 1] + dp[i]) % MOD;
			}
		}
		bw.write(dp[N] + "\n");
		bw.flush();
		bw.close();
		br.close();
	}

}
```