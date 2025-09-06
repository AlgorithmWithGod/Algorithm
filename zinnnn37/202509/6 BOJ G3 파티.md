```java
import java.io.*;
import java.util.*;

public class BJ_1238_파티 {

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static       StringTokenizer st;

	private static int N;
	private static int M;
	private static int X;

	private static int[]        aDist;
	private static int[]        dDist;
	private static List<Node>[] asc;
	private static List<Node>[] desc;

	static class Node implements Comparable<Node> {
		int end;
		int weight;

		public Node(int end, int weight) {
			this.end    = end;
			this.weight = weight;
		}

		@Override
		public int compareTo(Node o) {
			return Integer.compare(this.weight, o.weight);
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
		X = Integer.parseInt(st.nextToken());

		asc  = new List[N + 1];
		desc = new List[N + 1];
		for (int i = 1; i <= N; i++) {
			asc[i]  = new ArrayList<>();
			desc[i] = new ArrayList<>();
		}
		for (int i = 0; i < M; i++) {
			st = new StringTokenizer(br.readLine());

			int u = Integer.parseInt(st.nextToken());
			int v = Integer.parseInt(st.nextToken());
			int w = Integer.parseInt(st.nextToken());

			asc[u].add(new Node(v, w));
			desc[v].add(new Node(u, w));
		}
	}

	private static void sol() throws IOException {
		aDist = dijkstra(X, desc);
		dDist = dijkstra(X, asc);

		int maxTime = 0;
		for (int i = 1; i <= N; i++) {
			if (i != X) {
				maxTime = Math.max(maxTime, aDist[i] + dDist[i]);
			}
		}

		bw.write(maxTime + "");
		bw.flush();
		bw.close();
		br.close();
	}

	private static int[] dijkstra(int start, List<Node>[] graph) {
		PriorityQueue<Node> pq = new PriorityQueue<>();

		int[] dist = new int[N + 1];
		Arrays.fill(dist, Integer.MAX_VALUE);

		dist[start] = 0;
		pq.offer(new Node(start, 0));

		while (!pq.isEmpty()) {
			Node current   = pq.poll();
			int  curEnd    = current.end;
			int  curWeight = current.weight;

			if (curWeight > dist[curEnd]) continue;

			for (Node next : graph[curEnd]) {
				int nextEnd    = next.end;
				int nextWeight = next.weight;

				int newDist = dist[curEnd] + nextWeight;

				if (newDist < dist[nextEnd]) {
					dist[nextEnd] = newDist;
					pq.offer(new Node(nextEnd, newDist));
				}
			}
		}
		return dist;
	}
}
```