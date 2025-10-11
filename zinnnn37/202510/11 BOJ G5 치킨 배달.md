```java
import java.awt.*;
import java.io.*;
import java.util.ArrayList;
import java.util.List;
import java.util.StringTokenizer;

public class BJ_15686_치킨_배달 {

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static       StringTokenizer st;

	private static int N, M, ans, chickenCnt;
	private static int[][] map;
	private static int[]   selected;

	private static List<Point> houses;
	private static List<Point> chickens;

	public static void main(String[] args) throws IOException {
		init();
		sol(0, 0);

		bw.write(ans + "");
		bw.flush();
		bw.close();
		br.close();
	}

	private static void init() throws IOException {
		st  = new StringTokenizer(br.readLine());
		N   = Integer.parseInt(st.nextToken());
		M   = Integer.parseInt(st.nextToken());
		ans = Integer.MAX_VALUE;

		chickenCnt = 0;
		map        = new int[N][N];
		houses     = new ArrayList<>();
		chickens   = new ArrayList<>();

		for (int i = 0; i < N; i++) {
			st = new StringTokenizer(br.readLine());
			for (int j = 0; j < N; j++) {
				map[i][j] = Integer.parseInt(st.nextToken());

				if (map[i][j] == 1) {
					houses.add(new Point(i, j));
				} else if (map[i][j] == 2) {
					chickens.add(new Point(i, j));
					chickenCnt++;
				}
			}
		}
		selected = new int[M];
	}

	private static void sol(int depth, int start) throws IOException {
		if (depth == M) {
			measure();
			return;
		}

		for (int i = start; i < chickenCnt; i++) {
			selected[depth] = i;
			sol(depth + 1, i + 1);
		}
	}

	private static void measure() {
		int min = 0;
		for (Point h : houses) {
			int tmp = Integer.MAX_VALUE;
			for (int survived : selected) {
				Point c = chickens.get(survived);

				tmp = Math.min(tmp, Math.abs(h.x - c.x) + Math.abs(h.y - c.y));
			}
			min += tmp;
		}
		ans = Math.min(ans, min);
	}

}
```