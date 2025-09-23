```java
import java.io.*;
import java.util.ArrayList;
import java.util.List;
import java.util.StringTokenizer;

public class BJ_2660_회장뽑기 {

	private static final int INF = 987654321;

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static final StringBuilder   sb = new StringBuilder();
	private static       StringTokenizer st;

	private static int           N;
	private static int[][]       graph;
	private static List<Integer> candidate;

	public static void main(String[] args) throws IOException {
		init();
		sol();
	}

	private static void init() throws IOException {
		N = Integer.parseInt(br.readLine());

		graph = new int[N + 1][N + 1];
		for (int i = 1; i <= N; i++) {
			for (int j = 1; j <= N; j++) {
				if (i == j) continue;
				graph[i][j] = INF;
			}
		}

		candidate = new ArrayList<>();
		while (true) {
			st = new StringTokenizer(br.readLine());

			int u = Integer.parseInt(st.nextToken());
			int v = Integer.parseInt(st.nextToken());

			if (u == -1 && v == -1) break;

			graph[u][v] = 1;
			graph[v][u] = 1;
		}
	}

	private static void sol() throws IOException {
		for (int k = 1; k <= N; k++) {
			for (int i = 1; i <= N; i++) {
				for (int j = 1; j <= N; j++) {
					if (i == j || i == k || j == k) continue;

					if (graph[i][j] > graph[i][k] + graph[k][j]) {
						graph[i][j] = graph[i][k] + graph[k][j];
					}
				}
			}
		}

		int tmp = INF;
		for (int i = 1; i <= N; i++) {
			int max = 0;
			for (int j = 1; j <= N; j++) {
				if (graph[i][j] == INF) continue;

				max = Math.max(graph[i][j], max);
			}

			if (max == tmp) {
				candidate.add(i);
			} else if (max < tmp) {
				tmp = max;
				candidate.clear();
				candidate.add(i);
			}
		}

		sb.append(tmp).append(" ").append(candidate.size()).append("\n");
		for (int i : candidate) {
			sb.append(i).append(" ");
		}
		bw.write(sb.toString());
		bw.flush();
		bw.close();
		br.close();
	}

}
```