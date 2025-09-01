```java
import java.io.*;
import java.util.Arrays;
import java.util.StringTokenizer;

public class BJ_1106_호텔 {

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static       StringTokenizer st;

	private static int     C;
	private static int     N;
	private static int[]   dp;
	private static int[][] cost;

	public static void main(String[] args) throws IOException {
		init();
		sol();
	}

	private static void init() throws IOException {
		st = new StringTokenizer(br.readLine());
		C  = Integer.parseInt(st.nextToken());
		N  = Integer.parseInt(st.nextToken());

		cost = new int[N][2];
		for (int i = 0; i < N; i++) {
			st         = new StringTokenizer(br.readLine());
			cost[i][0] = Integer.parseInt(st.nextToken());
			cost[i][1] = Integer.parseInt(st.nextToken());
		}

		dp = new int[C + 100];
		Arrays.fill(dp, 987654321);
		dp[0] = 0;
	}

	private static void sol() throws IOException {
		for (int[] c : cost) {
			for (int i = c[1]; i < C + 100; i++) {
				dp[i] = Math.min(dp[i], dp[i - c[1]] + c[0]);
			}
		}
		bw.write(findMin() + "");
		bw.flush();
		bw.close();
		br.close();
	}

	private static int findMin() {
		int ans = dp[C];
		for (int i = C + 1; i < C + 100; i++) {
			ans = Math.min(ans, dp[i]);
		}
		return ans;
	}

}
```