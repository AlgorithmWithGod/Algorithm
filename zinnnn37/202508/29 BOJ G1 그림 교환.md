```java
import java.io.*;

public class Main {

	private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

	private static int     N;
	private static int     size;
	private static int[][] arr;
	private static int[][] dp;

	public static void main(String[] args) throws IOException {
		init();
		sol();
	}

	private static void init() throws IOException {
		N   = Integer.parseInt(br.readLine());
		arr = new int[N][N];

		for (int i = 0; i < N; i++) {
			String s = br.readLine();
			for (int j = 0; j < N; j++) {
				arr[i][j] = s.charAt(j) - '0';
			}
		}

		size = (int) Math.pow(2, N);
		dp   = new int[size][N];
	}

	private static void sol() throws IOException {
		int ans = dfs(0, 0, 0) + 1;
		bw.write(ans + "");
		bw.flush();
		bw.close();
		br.close();
	}

	private static int dfs(int buyer, int owners, int price) {
		// 현재 구매자가 그림 구매
		owners |= (1 << buyer);

		// 이미 구매 함
		if (dp[owners][buyer] != 0) {
			return dp[owners][buyer];
		}

		// 다음 구매자 구하기
		for (int i = 0; i < N; i++) {
			// 다음 구매자가 구매 가능 && 같거나 비싼 가격으로 구매 가능
			if ((owners & (1 << i)) == 0 && arr[buyer][i] >= price) {
				dp[owners][buyer] = Math.max(dp[owners][buyer], dfs(i, owners, arr[buyer][i]) + 1);
			}
		}
		return dp[owners][buyer];
	}

}
```