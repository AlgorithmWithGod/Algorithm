```java
import java.io.*;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.StringTokenizer;

public class BJ_15683_감시 {

	private static final int[]     dx  = { -1, 1, 0, 0 };
	private static final int[]     dy  = { 0, 0, -1, 1 };
	private static final int[][][] dir = {
			{ { 0 } },
			{ { 0 }, { 1 }, { 2 }, { 3 } }, // 1번 CCTV
			{ { 0, 1 }, { 2, 3 } }, // 2번
			{ { 0, 2 }, { 0, 3 }, { 1, 2 }, { 1, 3 } },
			{ { 0, 1, 2 }, { 0, 1, 3 }, { 1, 2, 3 }, { 0, 2, 3 } },
			{ { 0, 1, 2, 3 } }
	};

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static       StringTokenizer st;

	private static int N, M, res;
	private static int[][] map;

	private static int        cctvCnt;
	private static List<CCTV> cctvs = new ArrayList<>();

	static class CCTV {
		int x;
		int y;
		int type;

		public CCTV(int x, int y, int type) {
			this.x = x;
			this.y = y;
			this.type = type;
		}
	}

	public static void main(String[] args) throws IOException {
		init();
		sol(0, map);

		bw.write(res + "");
		bw.flush();
		bw.close();
		br.close();
	}

	public static void init() throws IOException {
		st = new StringTokenizer(br.readLine());
		N = Integer.parseInt(st.nextToken());
		M = Integer.parseInt(st.nextToken());

		res = Integer.MAX_VALUE;
		map = new int[N][M];

		for (int i = 0; i < N; i++) {
			st = new StringTokenizer(br.readLine());

			for (int j = 0; j < M; j++) {
				map[i][j] = Integer.parseInt(st.nextToken());

				if (1 <= map[i][j] && map[i][j] <= 5) {
					cctvs.add(new CCTV(i, j, map[i][j]));
				}
			}
		}

		cctvCnt = cctvs.size();
	}

	public static void sol(int depth, int[][] prev) {
		if (depth == cctvCnt) {
			res = Math.min(res, countBlind(prev));
			return;
		}

		int[][] copied = new int[N][M];

		CCTV cur    = cctvs.get(depth);
		int  type   = cur.type;
		int  rotate = dir[type].length;

		for (int i = 0; i < rotate; i++) {
			copy(copied, prev);

			for (int j = 0; j < dir[type][i].length; j++) {
				countWatched(cur.x, cur.y, dir[type][i][j], copied);
			}

			sol(depth + 1, copied);
		}
	}

	public static int countBlind(int[][] arr) {
		int blind = 0;
		for (int i = 0; i < N; i++) {
			for (int j = 0; j < M; j++) {
				if (arr[i][j] == 0) {
					blind++;
				}
			}
		}
		return blind;
	}

	public static int countWatched(int x, int y, int dir, int[][] copied) {
		int cnt = 0;
		while (true) {
			x += dx[dir];
			y += dy[dir];

			if (OOB(x, y) || copied[x][y] == 6) {
				return cnt;
			}

			if (copied[x][y] == 0) {
				cnt++;
				copied[x][y] = -1;
			}
		}
	}

	public static void copy(int[][] from, int[][] to) {
		for (int i = 0; i < N; i++) {
			from[i] = Arrays.copyOf(to[i], M);
		}
	}

	private static boolean OOB(int x, int y) {
		return x < 0 || N <= x || y < 0 || M <= y;
	}
}
```