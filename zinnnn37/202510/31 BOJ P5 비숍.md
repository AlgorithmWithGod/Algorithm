```java
import java.io.*;
import java.util.ArrayList;
import java.util.List;

public class BJ_1799_비숍 {

	private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

	private static int N, blackAns, whiteAns;
	private static boolean[] diag1, diag2; // 각각 \, / 대각선 비교
	private static List<Point> black, white;

	private static class Point {
		int x;
		int y;

		Point(int x, int y) {
			this.x = x;
			this.y = y;
		}
	}

	public static void main(String[] args) throws IOException {
		init();
		sol();
	}

	private static void init() throws IOException {
		N = Integer.parseInt(br.readLine());

		diag1 = new boolean[2 * N];
		diag2 = new boolean[2 * N];
		black = new ArrayList<>();
		white = new ArrayList<>();

		for (int i = 0; i < N; i++) {
			String s = br.readLine();
			for (int j = 0; j < N; j++) {
				char c = s.charAt(j * 2);

				if (c == '1') {
					if ((i + j) % 2 == 0) {
						black.add(new Point(i, j));
					} else {
						white.add(new Point(i, j));
					}
				}
			}
		}
	}

	private static void sol() throws IOException {
		// 검은색 칸만 탐색
		blackAns = 0;
		dfs(black, 0, 0);

		// 흰색 칸만 탐색
		whiteAns = 0;
		dfs(white, 0, 0);

		bw.write((blackAns + whiteAns) + "");
		bw.flush();
		bw.close();
		br.close();
	}

	private static void dfs(List<Point> list, int depth, int cnt) {
		if (list == black) {
			blackAns = Math.max(blackAns, cnt);
		} else {
			whiteAns = Math.max(whiteAns, cnt);
		}

		for (int i = depth; i < list.size(); i++) {
			Point p = list.get(i);
			// \은 x - y가 동일함 - 음수가 될 수 있으므로 N을 더해줌
			// /은 x + y가 동일함
			int d1 = p.x - p.y + N;
			int d2 = p.x + p.y;

			// 해당 대각선이 이미 탐색되었으면 pass
			if (diag1[d1] || diag2[d2]) continue;

			diag1[d1] = true;
			diag2[d2] = true;
			dfs(list, i + 1, cnt + 1);
			diag1[d1] = false;
			diag2[d2] = false;
		}
	}
}
```