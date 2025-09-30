```java
import java.io.*;
import java.util.Arrays;
import java.util.StringTokenizer;

public class BJ_12869_뮤탈리스크 {

	private static final int[][] dir = new int[][] {
			{ 9, 3, 1 },
			{ 9, 1, 3 },
			{ 3, 9, 1 },
			{ 3, 1, 9 },
			{ 1, 9, 3 },
			{ 1, 3, 9 }
	};

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static       StringTokenizer st;

	private static int       N;
	private static int[]     scv;
	private static int[][][] dp;

	public static void main(String[] args) throws IOException {
		init();
		sol();
	}

	private static void init() throws IOException {
		N = Integer.parseInt(br.readLine());

		scv = new int[3];
		st  = new StringTokenizer(br.readLine());
		for (int i = 0; i < N; i++) {
			scv[i] = Integer.parseInt(st.nextToken());
		}

		dp = new int[scv[0] + 1][scv[1] + 1][scv[2] + 1];

		for (int i = 0; i <= scv[0]; i++) {
			for (int j = 0; j <= scv[1]; j++) {
				Arrays.fill(dp[i][j], -1);
			}
		}
		dp[scv[0]][scv[1]][scv[2]] = 0;
	}

	private static void sol() throws IOException {
		for (int i = scv[0]; i >= 0; i--) {
			for (int j = scv[1]; j >= 0; j--) {
				for (int k = scv[2]; k >= 0; k--) {
					// 도달 불가
					if (dp[i][j][k] == -1) continue;

					for (int[] d : dir) {
						int ni = Math.max(i - d[0], 0);
						int nj = Math.max(j - d[1], 0);
						int nk = Math.max(k - d[2], 0);

						// 첫 방문 혹은 작은 수
						if (dp[ni][nj][nk] == -1 || dp[ni][nj][nk] > dp[i][j][k] + 1) {
							dp[ni][nj][nk] = dp[i][j][k] + 1;
						}
					}
				}
			}
		}
		bw.write(dp[0][0][0] + "");
		bw.flush();
		bw.close();
		br.close();
	}

}
```