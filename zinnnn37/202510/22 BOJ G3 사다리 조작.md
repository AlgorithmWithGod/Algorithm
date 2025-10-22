```java
import java.io.*;
import java.util.StringTokenizer;

public class BJ_15684_사다리_조작 {

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static       StringTokenizer st;

	private static int N, M, H;
	private static boolean[][] ladder;

	public static void main(String[] args) throws IOException {
		init();

		for (int target = 0; target <= 3; target++) {
			if (dfs(1, 1, 0, target)) {
				bw.write(target + "");
				bw.flush();
				bw.close();
				br.close();
				return;
			}
		}

		bw.write("-1");
		bw.flush();
		bw.close();
		br.close();
	}

	private static void init() throws IOException {
		st = new StringTokenizer(br.readLine());
		N = Integer.parseInt(st.nextToken());
		M = Integer.parseInt(st.nextToken());
		H = Integer.parseInt(st.nextToken());

		ladder = new boolean[H + 1][N + 1];
		for (int i = 0; i < M; i++) {
			st = new StringTokenizer(br.readLine());
			int a = Integer.parseInt(st.nextToken());
			int b = Integer.parseInt(st.nextToken());
			ladder[a][b] = true;
		}
	}

	private static boolean dfs(int h, int n, int cnt, int target) {
		if (cnt == target) {
			return check();
		}

		for (int i = h; i <= H; i++) {
			int colStart = (i == h ? n : 1);
			for (int j = colStart; j < N; j++) {
				if (canPlace(i, j)) {
					ladder[i][j] = true;
					if (dfs(i, j + 2, cnt + 1, target)) {
						return true;
					}
					ladder[i][j] = false;
				}
			}
		}

		return false;
	}

	private static boolean canPlace(int h, int n) {
		if (ladder[h][n]) return false;
		if (n > 1 && ladder[h][n - 1]) return false;
		if (n < N - 1 && ladder[h][n + 1]) return false;
		return true;
	}

	private static boolean check() {
		for (int start = 1; start <= N; start++) {
			int pos = start;

			for (int h = 1; h <= H; h++) {
				if (pos < N && ladder[h][pos]) {
					pos++;
				} else if (pos > 1 && ladder[h][pos - 1]) {
					pos--;
				}
			}

			if (pos != start) {
				return false;
			}
		}
		return true;
	}
}
```