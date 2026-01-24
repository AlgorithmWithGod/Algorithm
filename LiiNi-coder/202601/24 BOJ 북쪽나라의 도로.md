```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayDeque;
import java.util.ArrayList;
import java.util.Deque;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class Main{
	private static Map<Integer, List<int[]>> graph = new HashMap<>();
	private static int N = 0;
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		while(true){
			String line= br.readLine();
			if(line == null  || line.trim().isEmpty()){
				break;
			}
			String[] tokens = line.split(" ");
			int a = Integer.parseInt(tokens[0]);
			int b = Integer.parseInt(tokens[1]);
			int w = Integer.parseInt(tokens[2]);
			graph.putIfAbsent(a, new ArrayList<>());
			graph.putIfAbsent(b, new ArrayList<>());
			graph.get(a).add(new int[]{b, w});
			graph.get(b).add(new int[]{a, w});
			N = Math.max(N, a);
			N = Math.max(N, b);
		}
		//트리의 지름 : 아무점에서 최장거리 가지는 노드 구하고
		// 해당 노드에서 또 최장거리를 구한것이 트리의 지름
		int[] r1 = bfs(1);
		int[] r2 = bfs(r1[0]);
		System.out.println(r2[1]);
	}

	static int[] bfs(int start) {
		boolean[] visited = new boolean[N + 1];
		Deque<int[]> q = new ArrayDeque<>();
		q.offer(new int[]{start, 0});
		visited[start] = true;

		int far = start;
		int max = 0;

		while (!q.isEmpty()) {
			int[] cur = q.poll();
			int v = cur[0];
			int d = cur[1];
			if (d > max) {
				max = d;
				far = v;
			}
			for (int[] next : graph.get(v)) {
				int nv = next[0];
				int w = next[1];
				if (!visited[nv]) {
					visited[nv] = true;
					q.offer(new int[]{nv, d + w});
				}
			}
		}
		return new int[]{far, max};
	}
}
```
