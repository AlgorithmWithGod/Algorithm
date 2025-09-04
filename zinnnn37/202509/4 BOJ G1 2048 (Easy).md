```java
import java.io.*;
import java.util.Arrays;
import java.util.StringTokenizer;

public class BJ_12100_2048_Easy {

	private static final int UP    = 0;
	private static final int DOWN  = 1;
	private static final int LEFT  = 2;
	private static final int RIGHT = 3;

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static       StringTokenizer st;

	private static int         N;
	private static int         ans;
	private static int[]       order;
	private static int[][]     map;
	private static int[][]     copiedMap;
	private static boolean[][] visited;

	public static void main(String[] args) throws IOException {
		init();
		sol();
	}

	private static void init() throws IOException {
		N   = Integer.parseInt(br.readLine());
		ans = 0;

		order = new int[5];

		map       = new int[N][N];
		copiedMap = new int[N][N];
		visited   = new boolean[N][N];
		for (int i = 0; i < N; i++) {
			st = new StringTokenizer(br.readLine());
			for (int j = 0; j < N; j++) {
				map[i][j] = Integer.parseInt(st.nextToken());
			}
		}
	}

	private static void sol() throws IOException {
		dfs(0);

		bw.write(ans + "");
		bw.flush();
		bw.close();
		br.close();
	}

	private static void dfs(int depth) {
		if (depth == 5) {
			copyMap();
			playGame();
			updateMaxValue();
			return;
		}

		for (int i = 0; i < 4; i++) {
			order[depth] = i;
			dfs(depth + 1);
		}
	}

	private static void copyMap() {
		for (int i = 0; i < N; i++) {
			System.arraycopy(map[i], 0, copiedMap[i], 0, N);
		}
	}

	private static void playGame() {
		for (int d : order) {
			clearVisited();
			if (d == UP) {
				up();
			} else if (d == DOWN) {
				down();
			} else if (d == LEFT) {
				left();
			} else if (d == RIGHT) {
				right();
			}
		}
	}

	private static void up() {
		for (int j = 0; j < N; j++) {
			for (int i = 1; i < N; i++) {
				if (copiedMap[i][j] == 0) continue;

				int value = copiedMap[i][j];
				copiedMap[i][j] = 0;

				int k = i - 1;
				// 0이 아닌 블록이나 경계를 찾기
				while (k >= 0 && copiedMap[k][j] == 0) {
					k--;
				}

				if (k >= 0 && copiedMap[k][j] == value && !visited[k][j]) {
					// 합치기 가능
					copiedMap[k][j] = value * 2;
					visited[k][j]   = true;
				} else {
					// 합치기 불가능 - 빈 공간에 배치
					copiedMap[k + 1][j] = value;
				}
			}
		}
	}

	private static void down() {
		for (int j = 0; j < N; j++) {
			for (int i = N - 2; i >= 0; i--) {
				if (copiedMap[i][j] == 0) continue;

				int value = copiedMap[i][j];
				copiedMap[i][j] = 0;

				int k = i + 1;
				while (k < N && copiedMap[k][j] == 0) {
					k++;
				}

				if (k < N && copiedMap[k][j] == value && !visited[k][j]) {
					copiedMap[k][j] = value * 2;
					visited[k][j]   = true;
				} else {
					copiedMap[k - 1][j] = value;
				}
			}
		}
	}

	private static void left() {
		for (int i = 0; i < N; i++) {
			for (int j = 1; j < N; j++) {
				if (copiedMap[i][j] == 0) continue;

				int value = copiedMap[i][j];
				copiedMap[i][j] = 0;

				int k = j - 1;
				while (k >= 0 && copiedMap[i][k] == 0) {
					k--;
				}

				if (k >= 0 && copiedMap[i][k] == value && !visited[i][k]) {
					copiedMap[i][k] = value * 2;
					visited[i][k]   = true;
				} else {
					copiedMap[i][k + 1] = value;
				}
			}
		}
	}

	private static void right() {
		for (int i = 0; i < N; i++) {
			for (int j = N - 2; j >= 0; j--) {
				if (copiedMap[i][j] == 0) continue;

				int value = copiedMap[i][j];
				copiedMap[i][j] = 0;

				int k = j + 1;
				while (k < N && copiedMap[i][k] == 0) {
					k++;
				}

				if (k < N && copiedMap[i][k] == value && !visited[i][k]) {
					copiedMap[i][k] = value * 2;
					visited[i][k]   = true;
				} else {
					copiedMap[i][k - 1] = value;
				}
			}
		}
	}

	private static void updateMaxValue() {
		for (int i = 0; i < N; i++) {
			for (int j = 0; j < N; j++) {
				ans = Math.max(ans, copiedMap[i][j]);
			}
		}
	}

	private static void clearVisited() {
		for (int i = 0; i < N; i++) {
			Arrays.fill(visited[i], false);
		}
	}
}
```