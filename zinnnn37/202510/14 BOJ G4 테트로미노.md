```java
import java.io.*;
import java.util.StringTokenizer;

public class BJ_14500_테트로미노 {

	private static final int[] dx = { 0, 1, 0, -1 };
	private static final int[] dy = { 1, 0, -1, 0 };

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static       StringTokenizer st;

	private static int N, M, ans;
	private static int[][]     matrix;
	private static boolean[][] visited;

	public static void main(String[] args) throws IOException {
		init();
		sol();
	}

	private static void init() throws IOException {
		st  = new StringTokenizer(br.readLine());
		N   = Integer.parseInt(st.nextToken());
		M   = Integer.parseInt(st.nextToken());
		ans = 0;

		matrix = new int[N][M];
		for (int i = 0; i < N; i++) {
			st = new StringTokenizer(br.readLine());
			for (int j = 0; j < M; j++) {
				matrix[i][j] = Integer.parseInt(st.nextToken());
			}
		}

		visited = new boolean[N][M];
	}

	private static void sol() throws IOException {
		for (int i = 0; i < N; i++) {
			for (int j = 0; j < M; j++) {
				visited[i][j] = true;
				dfs(1, i, j, matrix[i][j]);
				visited[i][j] = false;
			}
		}
		bw.write(ans + "");
		bw.flush();
		bw.close();
		br.close();
	}

	private static void dfs(int depth, int cx, int cy, int tmp) throws IOException {
		if (depth == 4) {
			ans = Math.max(ans, tmp);
			return;
		}

		if (tmp + (4 - depth) * 1000 <= ans) {
			return;
		}

		for (int d = 0; d < 4; d++) {
			int nx = cx + dx[d];
			int ny = cy + dy[d];

			if (nx < 0 || N <= nx || ny < 0 || M <= ny || visited[nx][ny]) continue;

			// 凸 처리 - 다음칸으로 이동하지 않음으로써 중간 칸에서 분기 가능하도록 함
			if (depth == 2) {
				visited[nx][ny] = true;
				dfs(depth + 1, cx, cy, tmp + matrix[nx][ny]);
				visited[nx][ny] = false;
			}

			visited[nx][ny] = true;
			dfs(depth + 1, nx, ny, tmp + matrix[nx][ny]);
			visited[nx][ny] = false;
		}
	}

}
```