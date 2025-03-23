```java
import java.util.*;
import java.io.*;

public class Solution {
	static ArrayList<ArrayList<Integer>> graph;
	static boolean[] visited;
	static int V, E;
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		
		V = Integer.parseInt(st.nextToken());
		E = Integer.parseInt(st.nextToken());
		graph = new ArrayList<>(V+1);
		visited = new boolean[V+1];
		for (int i = 0; i< V+1; i++) {
			graph.add(new ArrayList<>());
		}
		
		for (int i = 0; i < E; i++) {
			st = new StringTokenizer(br.readLine());
			int a = Integer.parseInt(st.nextToken());
			int b = Integer.parseInt(st.nextToken());
			graph.get(a).add(b);
			graph.get(b).add(a);
		}
		connected(1);
		for (int i = 1; i < V+1; i++) {
			if (!visited[i]) {
				System.out.println("NO");
				return;
			}
		}
		int odd = 0, even = 0;
		for (int i = 1; i < V+1; i++) {
			if (graph.get(i).size() % 2 == 1) odd++;
			else even++;
		}
		if ((even == V-2 && odd == 2) || odd == 0) {
			System.out.println("YES");
		} else {
			System.out.println("NO");
		}
	}

	static void connected(int idx) {
		Queue<Integer> q = new LinkedList<>();
		q.add(idx);
		visited[idx] = true;
		while (!q.isEmpty()) {
			int curr = q.poll();
			for (int n : graph.get(curr)) {
				if (visited[n]) continue;
				visited[n] = true;
				q.add(n);
			}
		}
	}
}
```
