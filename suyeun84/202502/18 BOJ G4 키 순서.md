```java
import java.util.*;
import java.io.*;

public class Main {

	public static void main(String[] args) throws Exception {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		
		int N = Integer.parseInt(st.nextToken());
		int M = Integer.parseInt(st.nextToken());
		int answer = 0;
		ArrayList<ArrayList<Integer>> maxgraph = new ArrayList<>(N+1);
		ArrayList<ArrayList<Integer>> mingraph = new ArrayList<>(N+1);
		for (int i = 0; i < N+1; i++) {
			maxgraph.add(new ArrayList<>());
			mingraph.add(new ArrayList<>());
		}
		for (int i = 0 ; i < M; i++) {
			st = new StringTokenizer(br.readLine());
			int a = Integer.parseInt(st.nextToken());
			int b = Integer.parseInt(st.nextToken());
			mingraph.get(b).add(a);
			maxgraph.get(a).add(b);
		}
		for (int i = 1; i <= N; i++) {
			Queue<Integer> q = new LinkedList<>();
			q.add(i);
			boolean[] visited = new boolean[N+1];
			int mincnt = 0;
      visited[i] = true;
			while (!q.isEmpty()) {
				int curr = q.poll();
				for (int k : mingraph.get(curr)) {
					if (!visited[k]) {
						q.add(k);
						visited[k] = true;
						mincnt++;
					}
				}
			}
			int maxcnt = 0;
			q.add(i);
			Arrays.fill(visited, false);
      visited[i] = true;
			while (!q.isEmpty()) {
				int curr = q.poll();
				for (int k : maxgraph.get(curr)) {
					if (!visited[k]) {
						q.add(k);
						visited[k] = true;
						maxcnt++;
					}
				}
			}
			if (mincnt + maxcnt == N-1) answer++;
		}
		System.out.println(answer);
	}
}
```
