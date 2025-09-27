```java
import java.io.*;
import java.util.StringTokenizer;

public class BJ_1915_가장_큰_정사각형 {

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static       StringTokenizer st;

	private static int N, M;
	private static int[][] map;
	private static int[][] dp;
	private static int     maxVal;

	public static void main(String[] args) throws IOException {
		init();
		sol();
	}

	private static void init() throws IOException {
		st = new StringTokenizer(br.readLine());
		N  = Integer.parseInt(st.nextToken());
		M  = Integer.parseInt(st.nextToken());

		map = new int[N + 1][M + 1];
		dp  = new int[N + 1][M + 1];
		for (int i = 1; i <= N; i++) {
			String s = br.readLine();
			for (int j = 1; j <= M; j++) {
				map[i][j] = s.charAt(j - 1) - '0';
			}
		}
		maxVal = 0;
	}

	private static void sol() throws IOException {
		for (int i = 1; i <= N; i++) {
			for (int j = 1; j <= M; j++) {
				if (map[i][j] == 0) {
					dp[i][j] = 0;
					continue;
				}
				dp[i][j] = Math.min(dp[i - 1][j - 1], Math.min(dp[i - 1][j], dp[i][j - 1])) + 1;
				maxVal   = Math.max(maxVal, dp[i][j]);
			}
		}
		bw.write((maxVal * maxVal) + "\n");
		bw.flush();
		bw.close();
		br.close();
	}

}
```