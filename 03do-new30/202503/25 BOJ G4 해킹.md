```java
import java.util.*;
import java.io.*;

public class Main {
	
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static int n, d, c;
	static List<Info>[] graph; // 인접 리스트
	
	static class Info implements Comparable<Info> {
		int id;
		int sec;
		public Info(int id, int sec) {
			this.id = id;
			this.sec = sec;
		}
		@Override
		public int compareTo(Info o) {
			return Integer.compare(this.sec, o.sec);
		}
	}
	
	public static void main(String[] args) throws IOException {
		int T = Integer.parseInt(br.readLine());
		for (int tc = 1; tc <= T; tc++) {
			input();
			// 총 감염되는 컴퓨터 수, 마지막 컴퓨터가 감염되기까지 걸리는 시간
			dijkstra(c);
		}
		br.close();
	}
	
	private static void dijkstra(int start) {
		PriorityQueue<Info> pq = new PriorityQueue<>();
		
		int[] dist = new int[n+1];
		for (int i = 0; i < n+1; i++) {
			dist[i] = -1;
		}
		dist[start] = 0;
		pq.add(new Info(start, 0));
		
		while (!pq.isEmpty()) {
			Info info = pq.poll();
			int current = info.id;
			if (dist[current] < info.sec) continue; // 이미 더 빠르게 방문한 적이 있으면 skip
			for (Info next : graph[current]) {
				if (dist[next.id] == -1 || dist[next.id] > dist[current] + next.sec ) { 
					dist[next.id] = dist[current] + next.sec; 
					pq.add(next);
				}
			}
		}
		
		int cnt = 0;
		int time = -1;
		for (int i = 1; i <= n; i++) {
			if (dist[i] == -1) { continue; }
			cnt++;
			time = Integer.max(time, dist[i]);
		}
		// 총 감염되는 컴퓨터 수
		// 감염되기까지 걸리는 시간
		System.out.println(cnt + " " + time);
	}
	
	private static void input() throws IOException {
		StringTokenizer st = new StringTokenizer(br.readLine());
		n = Integer.parseInt(st.nextToken());
		d = Integer.parseInt(st.nextToken());
		c = Integer.parseInt(st.nextToken());
		graph = new List[n+1];
		for (int i = 1; i < n+1; i++) {
			graph[i] = new ArrayList<>();
		}
		for (int i = 0; i < d; i++) {
			st = new StringTokenizer(br.readLine());
			// 컴퓨터 a가 컴퓨터 b를 의존하며, 컴퓨터 b가 감염되면 s초 후 컴퓨터 a도 감염된다.
			int a = Integer.parseInt(st.nextToken());
			int b = Integer.parseInt(st.nextToken());
			int s = Integer.parseInt(st.nextToken());
			graph[b].add(new Info(a, s));
		}
	}
}

```
