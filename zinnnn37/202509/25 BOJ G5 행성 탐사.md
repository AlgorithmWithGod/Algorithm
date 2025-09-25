```java
import java.io.*;
import java.util.HashMap;
import java.util.Map;
import java.util.StringTokenizer;

public class BJ_5549_행성_탐사 {

	private static final Map<Character, Integer> MAP = new HashMap<>();

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static final StringBuilder   sb = new StringBuilder();
	private static       StringTokenizer st;
	private static       int             M, N, K;
	private static int[][][] dp;

	// Java 8
	static {
		MAP.put('J', 0);
		MAP.put('O', 1);
		MAP.put('I', 2);
	}

	public static void main(String[] args) throws IOException {
		init();
		sol();
	}

	private static void init() throws IOException {
		st = new StringTokenizer(br.readLine());
		M  = Integer.parseInt(st.nextToken());
		N  = Integer.parseInt(st.nextToken());
		K  = Integer.parseInt(br.readLine());

		dp = new int[M + 1][N + 1][3]; // J, O, I일때 누적합

		for (int i = 1; i <= M; i++) {
			String s = br.readLine();
			for (int j = 1; j <= N; j++) {
				char c = s.charAt(j - 1);

				// prefix
				dp[i][j][0] = dp[i - 1][j][0] + dp[i][j - 1][0] - dp[i - 1][j - 1][0];
				dp[i][j][1] = dp[i - 1][j][1] + dp[i][j - 1][1] - dp[i - 1][j - 1][1];
				dp[i][j][2] = dp[i - 1][j][2] + dp[i][j - 1][2] - dp[i - 1][j - 1][2];

				dp[i][j][MAP.get(c)]++;
			}
		}
	}

	private static void sol() throws IOException {
		while (K-- > 0) {
			st = new StringTokenizer(br.readLine());

			int x1 = Integer.parseInt(st.nextToken());
			int y1 = Integer.parseInt(st.nextToken());
			int x2 = Integer.parseInt(st.nextToken());
			int y2 = Integer.parseInt(st.nextToken());

			for (int i = 0; i < 3; i++) {
				sb.append(dp[x2][y2][i] - dp[x1 - 1][y2][i] - dp[x2][y1 - 1][i] + dp[x1 - 1][y1 - 1][i]).append(" ");
			}
			sb.append("\n");
		}
		bw.write(sb.toString());
		bw.flush();
		bw.close();
		br.close();
	}

}
```