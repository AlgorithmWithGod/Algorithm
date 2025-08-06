```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.PriorityQueue;

public class Main {
	private static BufferedReader br;
	private static int m;
	private static int n;

	static class Node implements Comparable<Node> {
		int v;
		int w;
		boolean prevDash;

		public Node(int v, int w) {
			this.v = v;
			this.w = w;
			this.prevDash = false;
		}

		public Node(int v, int w, boolean prevDash) {
			this.v = v;
			this.w = w;
			this.prevDash = prevDash;
		}

		@Override
		public int compareTo(Main.Node o) {
			return this.w - o.w;
		}
	}

	public static int[] dijkstra(List<List<Node>> graph, int start) {
		int n = graph.size();
		int[] dist = new int[n];
		Arrays.fill(dist, Integer.MAX_VALUE);
		dist[start] = 0;
		PriorityQueue<Node> pq = new PriorityQueue<>();
		pq.offer(new Node(start, 0));

		while (!pq.isEmpty()) {
			Node cn = pq.poll();
			int cv = cn.v;
			int cw = cn.w;
			if (dist[cv] < cw) continue;

			for (Node neighbor : graph.get(cv)) {
				int nv = neighbor.v;
				int nw = neighbor.w;
				if (dist[nv] > dist[cv] + nw) {
					dist[nv] = dist[cv] + nw;
					pq.offer(new Node(nv, dist[nv]));
				}
			}
		}
		return dist;
	}

	//달빛늑대 다익스트라
	public static int[][] dijkstraWolf(List<List<Node>> graph, int start) {
		int[][] dist = new int[2][graph.size()];
		for (int i = 0; i < 2; i++) {
			Arrays.fill(dist[i], Integer.MAX_VALUE);
		}
		PriorityQueue<Node> pq = new PriorityQueue<>();
		dist[0][start] = 0;
		pq.offer(new Node(start, 0, false));

		while (!pq.isEmpty()) {
			Node cn = pq.poll();
			int cv = cn.v;
			int cw = cn.w;
			boolean prevDash = cn.prevDash;
			int state = prevDash ? 1 : 0;
			if (dist[state][cv] < cw) continue;

			for (Node neighbor : graph.get(cv)) {
				int nv = neighbor.v;
				int nw = neighbor.w;
				int nextW = prevDash ? cw + nw : cw + nw / 2;
				if (dist[1 - state][nv] > nextW) {
					dist[1 - state][nv] = nextW;
					pq.offer(new Node(nv, nextW, !prevDash));
				}
			}
		}

		return dist;
	}

	public static void main(String[] args) throws IOException {
		br = new BufferedReader(new InputStreamReader(System.in));

		String[] temp = br.readLine().split(" ");
		n = Integer.parseInt(temp[0]);
		m = Integer.parseInt(temp[1]);

		List<List<Node>> graph = new ArrayList<>();
		for (int i = 0; i <= n; i++) {
			graph.add(new ArrayList<Node>());
		}
		for (int i = 0; i < m; i++) {
			temp = br.readLine().split(" ");
			int a = Integer.parseInt(temp[0]);
			int b = Integer.parseInt(temp[1]);
			int w = Integer.parseInt(temp[2]);
			graph.get(a).add(new Node(b, w*2));//계산 용이를 위해 애초에 곱하기 2
			graph.get(b).add(new Node(a, w*2));
		}

		// 달빛여우 다익 진행
		int[] foxDist = dijkstra(graph, 1);

		// 달빛늑대 다익진행(2차원 dist배열 사용)
		int[][] wolfDist = dijkstraWolf(graph, 1);

		int count = 0;
		for (int i = 2; i <= n; i++) {
			int wolfMin = Math.min(wolfDist[0][i], wolfDist[1][i]);
			if (foxDist[i] < wolfMin) {
				count++;
			}
		}

		System.out.println(count);
		br.close();
	}
}

```
