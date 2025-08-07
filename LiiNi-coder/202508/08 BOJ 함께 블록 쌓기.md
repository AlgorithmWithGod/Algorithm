```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;
import java.util.StringTokenizer;

public class Main {
	private static int N;
  private static int M;
  private static int H;
	private static int[][] blocks;
	private static int[][] dp;
	private static final int MOD = 10007;
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());

		N = Integer.parseInt(st.nextToken());
		M = Integer.parseInt(st.nextToken());
		H = Integer.parseInt(st.nextToken());

		blocks = new int[N][];
		for (int i = 0; i < N; i++) {
			st = new StringTokenizer(br.readLine());
			int[] temp = new int[st.countTokens()];
			for (int j = 0; j < temp.length; j++) {
				temp[j] = Integer.parseInt(st.nextToken());
			}
			blocks[i] = temp;
		}

		dp = new int[N + 1][H + 1];
		for (int i = 0; i <= N; i++) {
			for (int j = 0; j <= H; j++) {
				dp[i][j] = -1;
			}
		}
		System.out.println(dfs(0, 0));
	}

	private static int dfs(int i, int h) {
		if (h > H) return 0;
		if (i == N) return h == H ? 1 : 0;
		if (dp[i][h] != -1) return dp[i][h];
		int result = dfs(i + 1, h);
		for (int b : blocks[i]) {
			if (h + b <= H) {
				result += dfs(i + 1, h + b);
				//맨 마지막에 나누지말고 미리 빼버리기
				if (result >= MOD)
					result -= MOD;
			}
		}
		dp[i][h] = result;
		return result;
	}
}
```
