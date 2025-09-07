```java
import java.io.*;
import java.util.*;

public class BJ_13911_집_구하기 {

	private static final long INF = 9876543210L;

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static       StringTokenizer st;

	private static int V, E;
	private static int M, x;
	private static int S, y;

	private static long[]    mcdonalds;
	private static long[]    starbucks;
	private static boolean[] isMcdonalds;
	private static boolean[] isStarbucks;

	private static Queue<Node>  pq;
	private static List<Node>[] graph;

	private static class Node implements Comparable<Node> {
		int  from;
		int  to;
		long dist;

		Node(int from, int to, long dist) {
			this.from = from;
			this.to   = to;
			this.dist = dist;
		}

		@Override
		public int compareTo(Node o) {
			return Long.compare(this.dist, o.dist);
		}
	}

	public static void main(String[] args) throws IOException {
		init();
		sol();
	}

	private static void init() throws IOException {
		st = new StringTokenizer(br.readLine());
		V  = Integer.parseInt(st.nextToken());
		E  = Integer.parseInt(st.nextToken());

		graph = new List[V + 1];
		for (int i = 1; i <= V; i++) {
			graph[i] = new ArrayList<>();
		}

		for (int i = 1; i <= E; i++) {
			st = new StringTokenizer(br.readLine());

			int from   = Integer.parseInt(st.nextToken());
			int to     = Integer.parseInt(st.nextToken());
			int weight = Integer.parseInt(st.nextToken());

			graph[from].add(new Node(from, to, weight));
			graph[to].add(new Node(to, from, weight));
		}

		mcdonalds   = new long[V + 1];
		starbucks   = new long[V + 1];
		isMcdonalds = new boolean[V + 1];
		isStarbucks = new boolean[V + 1];

		pq = new PriorityQueue<>();
	}

	private static void sol() throws IOException {
		// Multisource Dijkstra
		st = new StringTokenizer(br.readLine());
		M  = Integer.parseInt(st.nextToken());
		x  = Integer.parseInt(st.nextToken());
		dijkstra(mcdonalds, isMcdonalds, M);

		// Multisource Dijkstra
		st = new StringTokenizer(br.readLine());
		S  = Integer.parseInt(st.nextToken());
		y  = Integer.parseInt(st.nextToken());
		dijkstra(starbucks, isStarbucks, S);

		long ans = INF;
		for (int i = 1; i <= V; i++) {
			if (!isMcdonalds[i] && !isStarbucks[i] && mcdonalds[i] <= x && starbucks[i] <= y) {
				ans = Math.min(ans, mcdonalds[i] + starbucks[i]);
			}
		}
		bw.write((ans == INF ? -1 : ans) + "");
		bw.flush();
		bw.close();
		br.close();
	}

	private static void dijkstra(long[] dist, boolean[] isStore, int cnt) throws IOException {
		pq.clear();
		Arrays.fill(dist, INF);

		st = new StringTokenizer(br.readLine());
		for (int i = 0; i < cnt; i++) {
			int start = Integer.parseInt(st.nextToken());
			isStore[start] = true;
			dist[start]    = 0;
			pq.offer(new Node(start, start, 0));
		}

		while (!pq.isEmpty()) {
			Node cur = pq.poll();

			if (cur.dist > dist[cur.to]) continue;

			for (Node n : graph[cur.to]) {
				long nDist = dist[cur.to] + n.dist;

				if (nDist < dist[n.to]) {
					dist[n.to] = nDist;
					pq.offer(new Node(n.from, n.to, nDist));
				}
			}
		}
	}

}
```