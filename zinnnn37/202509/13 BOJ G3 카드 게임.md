```java
import java.io.*;
import java.util.Arrays;
import java.util.StringTokenizer;

public class BJ_11062_카드_게임 {

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static final StringBuilder   sb = new StringBuilder();
	private static       StringTokenizer st;

	private static int N;

	private static int[]     cards   = new int[1001];
	private static boolean[] visited = new boolean[1001];
	private static int[][]   dp      = new int[1001][1001];

	public static void main(String[] args) throws IOException {
		int T = Integer.parseInt(br.readLine());

		while (T-- > 0) {
			init();
			sol();
		}
		bw.write(sb.toString());
		bw.flush();
		bw.close();
		br.close();
	}

	private static void init() throws IOException {
		N = Integer.parseInt(br.readLine());

		Arrays.fill(cards, 0);
		Arrays.fill(visited, false);
		for (int i = 0; i < N; i++) {
			Arrays.fill(dp[i], 0);
		}

		st = new StringTokenizer(br.readLine());
		for (int i = 0; i < N; i++) {
			cards[i] = Integer.parseInt(st.nextToken());
		}
	}

	private static void sol() throws IOException {
		game(0, 0, N - 1);

		sb.append(dp[0][N - 1]).append("\n");
	}

	private static int game(int depth, int left, int right) {
		if (right < left) return 0;
		if (dp[left][right] != 0) return dp[left][right];

		if (depth % 2 == 0) {
			return dp[left][right] = Math.max(game(depth + 1, left + 1, right) + cards[left]
					, game(depth + 1, left, right - 1) + cards[right]);
		} else {
			return dp[left][right] = Math.min(game(depth + 1, left + 1, right)
					, game(depth + 1, left, right - 1));
		}
	}

}
```