```java
import java.io.*;
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
import java.util.StringTokenizer;

public class BJ_8980_택배 {

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static       StringTokenizer st;

	private static int N, C, M, delivered, loaded;
	private static int[]        packageLoaded;
	private static List<Node>[] graph;

	private static class Node implements Comparable<Node> {
		int to;
		int packages;

		Node(int to, int packages) {
			this.to = to;
			this.packages = packages;
		}

		@Override
		public int compareTo(Node o) {
			return Integer.compare(this.to, o.to);
		}
	}

	public static void main(String[] args) throws IOException {
		init();
		sol();
	}

	private static void init() throws IOException {
		st = new StringTokenizer(br.readLine());

		N = Integer.parseInt(st.nextToken());
		C = Integer.parseInt(st.nextToken());
		M = Integer.parseInt(br.readLine());

		packageLoaded = new int[N + 1];

		graph = new List[N + 1];
		for (int i = 1; i <= N; i++) {
			graph[i] = new ArrayList<>();
		}

		for (int i = 0; i < M; i++) {
			st = new StringTokenizer(br.readLine());

			int from     = Integer.parseInt(st.nextToken());
			int to       = Integer.parseInt(st.nextToken());
			int packages = Integer.parseInt(st.nextToken());

			graph[from].add(new Node(to, packages));
		}

		for (int i = 1; i <= N; i++) {
			Collections.sort(graph[i]);
		}
	}

	private static void sol() throws IOException {
		for (int i = 1; i <= N; i++) {
			delivered += packageLoaded[i];
			loaded -= packageLoaded[i];

			for (int j = 0; j < graph[i].size(); j++) {
				Node cur = graph[i].get(j);

				if (loaded + cur.packages <= C) {
					loaded += cur.packages;
					packageLoaded[cur.to] += cur.packages;
				} else {
					int left = cur.packages - (C - loaded);
					for (int k = N; k >= cur.to; k--) {
						int diff = Math.min(left, packageLoaded[k]);

						packageLoaded[k] -= diff;
						left -= diff;
						loaded += diff;

						if (left == 0) break;
					}
					packageLoaded[cur.to] += cur.packages - left;
				}
			}
		}
		bw.write(delivered + "");
		bw.flush();
		bw.close();
		br.close();
	}

}
```