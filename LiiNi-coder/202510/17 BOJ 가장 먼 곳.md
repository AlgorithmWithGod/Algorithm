```java
import java.util.*;
import java.io.*;

class Main {

	static class Node implements Comparable<Node> {
		int to, weight;

		Node(int to, int weight) {
			this.to = to;
			this.weight = weight;
		}

		@Override
		public int compareTo(Node o){
			return this.weight - o.weight;
		}
	}

	static int N, M;
	static List<Node>[] Graph;
	static int[] Friends = new int[3];
	static final int INF = Integer.MAX_VALUE;

	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st;

		N = Integer.parseInt(br.readLine());
		st = new StringTokenizer(br.readLine());
		for(int i = 0; i < 3; i++)
			Friends[i] = Integer.parseInt(st.nextToken());

		M = Integer.parseInt(br.readLine());
		Graph = new ArrayList[N + 1];
		for(int i = 1; i <= N; i++)
			Graph[i] = new ArrayList<>();

		for (int i = 0; i < M; i++) {
			st = new StringTokenizer(br.readLine());
			int a = Integer.parseInt(st.nextToken());
			int b = Integer.parseInt(st.nextToken());
			int c = Integer.parseInt(st.nextToken());
			Graph[a].add(new Node(b, c));
			Graph[b].add(new Node(a, c));
		}

		int[][] dist = new int[3][N + 1];
		for(int i = 0; i < 3; i++){
			dist[i] = dijkstra(Friends[i]);
		}
		int answer = 0;
		int maxMinDist = -1;

		for(int i = 1; i <= N; i++){
			int minDist = Math.min(dist[0][i], Math.min(dist[1][i], dist[2][i]));
			if (minDist > maxMinDist) {
				maxMinDist = minDist;
				answer = i;
			}
		}


		System.out.println(answer);
		br.close();
	}

	private static int[] dijkstra(int start) {
		int[] dist = new int[N + 1];
		Arrays.fill(dist, INF);
		dist[start] = 0;

		PriorityQueue<Node> pq = new PriorityQueue<>();
		pq.offer(new Node(start, 0));
		while(!pq.isEmpty()){
			Node cur = pq.poll();
			if(cur.weight > dist[cur.to])
				continue;

			for(Node next : Graph[cur.to]){
				int cost = cur.weight + next.weight;
				if(cost < dist[next.to]){
					dist[next.to] = cost;
					pq.offer(new Node(next.to, cost));
				}
			}
		}
		return dist;
	}
}

```
