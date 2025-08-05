```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main {
	private static BufferedReader br;

	public static void main(String[] args) throws IOException {
		br = new BufferedReader(new InputStreamReader(System.in));
		String[] temp = br.readLine().split(" ");
		int n = Integer.parseInt(temp[0]);
		int m = Integer.parseInt(temp[1]);

		int[][] map = new int[n][m];
		for (int i = 0; i < n; i++) {
			temp = br.readLine().split(" ");
			for (int j = 0; j < m; j++) {
				map[i][j] = Integer.parseInt(temp[j]);
			}
		}

		int[][][] dp = new int[n][m + 2][3];
		int INF = Integer.MAX_VALUE;

		for (int c = 1; c <= m; c++) {
			for (int d = 0; d < 3; d++) {
				dp[0][c][d] = map[0][c - 1]; // map은 0-based
			}
		}
		for (int r = 1; r < n; r++) {
			for (int c = 1; c <= m; c++) {
				for (int dc : new int[] { -1, 0, 1 }) {
					int dp2index = dc + 1;
					int targetC = c + dc;
					if (targetC < 1 || targetC > m) {
						dp[r][c][dp2index] = INF;
						continue;
					}

					int minPrev = INF;
					for (int prevD = 0; prevD < 3; prevD++) {
						if (prevD == dp2index) continue; // 같은 방향 연속 이동 금지
						minPrev = Math.min(minPrev, dp[r - 1][targetC][prevD]);
					}
					if (minPrev == INF)
						dp[r][c][dp2index] = INF;
					else
						dp[r][c][dp2index] = minPrev + map[r][c - 1];
				}
			}
		}

		int answer = INF;
		for (int c = 1; c <= m; c++) {
			for (int d = 0; d < 3; d++) {
				answer = Math.min(answer, dp[n - 1][c][d]);
			}
		}
		System.out.println(answer);
	}
}
```
