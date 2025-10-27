```java
import java.io.*;
import java.util.*;

public class BJ_14938_서강그라운드 {

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static       StringTokenizer st;

	private static int N, M, R, tmp, ans;
	private static int[] dist, vals;
	private static List<Node>[] graph;
	private static Queue<Node>  q;

	private static class Node implements Comparable<Node> {
		int to;
		int dist;

		public Node(int to, int dist) {
			this.to = to;
			this.dist = dist;
		}

		@Override
		public int compareTo(Node o) {
			return Integer.compare(this.dist, o.dist);
		}
	}

	public static void main(String[] args) throws IOException {
		init();
		sol();
	}

	private static void init() throws IOException {
		st = new StringTokenizer(br.readLine());

		N = Integer.parseInt(st.nextToken());
		M = Integer.parseInt(st.nextToken());
		R = Integer.parseInt(st.nextToken());

		ans = 0;
		vals = new int[N + 1];
		st = new StringTokenizer(br.readLine());
		for (int i = 1; i <= N; i++) {
			vals[i] = Integer.parseInt(st.nextToken());
		}

		graph = new List[N + 1];
		for (int i = 1; i <= N; i++) {
			graph[i] = new ArrayList<>();
		}

		for (int i = 0; i < R; i++) {
			st = new StringTokenizer(br.readLine());

			int u = Integer.parseInt(st.nextToken());
			int v = Integer.parseInt(st.nextToken());
			int w = Integer.parseInt(st.nextToken());

			graph[u].add(new Node(v, w));
			graph[v].add(new Node(u, w));
		}

		q = new PriorityQueue<>();
		dist = new int[N + 1];
	}

	private static void sol() throws IOException {
		for (int i = 1; i <= N; i++) {
			dijkstra(i);

			tmp = 0;
			for (int j = 1; j <= N; j++) {
				if (dist[j] <= M) {
					tmp += vals[j];
				}
			}
			ans = Math.max(ans, tmp);
		}
		bw.write(ans + "\n");
		bw.flush();
		bw.close();
		br.close();
	}

	private static void dijkstra(int start) {
		q.clear();
		Arrays.fill(dist, Integer.MAX_VALUE);
		dist[start] = 0;

		q.offer(new Node(start, 0));

		while (!q.isEmpty()) {
			Node cur = q.poll();

			if (dist[cur.to] < cur.dist) continue;

			for (Node next : graph[cur.to]) {
				int newDist = dist[cur.to] + next.dist;

				if (newDist < dist[next.to]) {
					dist[next.to] = newDist;
					q.offer(new Node(next.to, newDist));
				}
			}
		}
	}

}
```