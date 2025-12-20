```java
import java.io.*;
import java.util.*;

public class Main {
	static class Edge {
		int to;
		int cost;
		Edge(int to, int cost){
			this.to = to;
			this.cost = cost;
		}
	}

	static final int INF = 100_000_000;
	static ArrayList<Edge>[] Graph;

	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		int N = Integer.parseInt(st.nextToken());
		int E = Integer.parseInt(st.nextToken());

		Graph = new ArrayList[N + 1];
		for(int i = 1; i <= N; i++){
			Graph[i] = new ArrayList<>();
		}
		for(int i = 0; i < E; i++){
			st = new StringTokenizer(br.readLine());
			int a = Integer.parseInt(st.nextToken());
			int b = Integer.parseInt(st.nextToken());
			int c = Integer.parseInt(st.nextToken());
			Graph[a].add(new Edge(b, c));
			Graph[b].add(new Edge(a, c));
		}
		st = new StringTokenizer(br.readLine());
		int A = Integer.parseInt(st.nextToken());
		int B = Integer.parseInt(st.nextToken());
		int[] dist1 = dikstra(1, N);
		int[] distA = dikstra(A, N);
		int[] distB = dikstra(B, N);

		long path1 = (long)dist1[A] + distA[B] + distB[N];
		long path2 = (long)dist1[B] + distB[A] + distA[N];
		long answer = Math.min(path1, path2);
		System.out.println((answer >= INF) ? -1 : answer);
	}

	private static int[] dikstra(int start, int N){
		int[] dist = new int[N + 1];
		Arrays.fill(dist, INF);
		dist[start] = 0;

		PriorityQueue<int[]> pq = new PriorityQueue<>(
			(a, b) -> a[1] - b[1]
		);
		pq.offer(new int[]{start, 0});

		while(!pq.isEmpty()){
			int[] cur = pq.poll();
			int now = cur[0];
			int cost = cur[1];

			if(cost > dist[now])
				continue;

			for(Edge e : Graph[now]){
				int next = e.to;
				int nextCost = cost + e.cost;
				if(nextCost < dist[next]){
					dist[next] = nextCost;
					pq.offer(new int[]{next, nextCost});
				}
			}
		}
		return dist;
	}
}

```
