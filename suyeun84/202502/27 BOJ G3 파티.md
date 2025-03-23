```java
import java.util.*;
import java.io.*;

public class boj1238 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
	static StringTokenizer st;
	
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	static void end() throws Exception {bw.flush();bw.close();br.close();}
	
	static ArrayList<ArrayList<Node>> graph = new ArrayList<>();
	static int N, M, X;
	
	public static void main(String[] args) throws Exception {
		nextLine();
		N = nextInt();
		M = nextInt();
		X = nextInt();
		int S, E, T, answer = 0;
		for (int i = 0; i < N+1; i++) graph.add(new ArrayList<>());
		
		for (int i = 0; i < M; i++) {
			nextLine();
			S = nextInt();
			E = nextInt();
			T = nextInt();
			graph.get(S).add(new Node(T, E));
		}
		
		for (int i = 1; i < N+1; i++) {
			answer = Math.max(answer, dijkstra(i, X) + dijkstra(X, i));
		}
		bw.write(answer+"\n");
		end();
	}
	
	static int dijkstra(int start, int target) {
		if (start == target) return 0;
		PriorityQueue<Node> pq = new PriorityQueue<>((o1, o2) -> o1.t-o2.t);
		int[] dist = new int[N+1];
		Arrays.fill(dist, Integer.MAX_VALUE);
		dist[start] = 0;
		pq.add(new Node(0, start));
		while (!pq.isEmpty()) {
			Node curr = pq.poll(); //시간 가장 작은 것
			if (dist[curr.e] < curr.t) continue;
			dist[curr.e] = curr.t;
			for (Node n : graph.get(curr.e)) {
				if (n.t+dist[curr.e] >= dist[n.e]) continue;
				pq.add(new Node(n.t+dist[curr.e], n.e));
			}
		}
		return dist[target];
	}

	static class Node {
		int t;
		int e;
		public Node(int t, int e) {
			this.t = t;
			this.e = e;
		}
	}
}
```
