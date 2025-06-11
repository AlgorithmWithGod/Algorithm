```java
import java.util.*;
import java.io.*;

public class boj1005 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	
	public static void main(String[] args) throws Exception {
		nextLine();
		int T = nextInt();
		for (int tc = 0; tc < T; tc++) {
			nextLine();
			int N = nextInt(); // 건물 개수 (1~N)
			int K = nextInt(); // 건설순서 규칙의 개수
			int[] time = new int[N+1]; // 건물당 걸리는 시간
			int[] answer = new int[N+1];
			int[] degree = new int[N+1];
			ArrayList<ArrayList<Integer>> graph = new ArrayList<>();
			for (int i = 0; i <= N; i++) graph.add(new ArrayList<Integer>());
			nextLine();
			for (int i = 1; i <= N; i++) time[i] = nextInt();
			for (int i = 0; i < K; i++) {
				nextLine();
				int a = nextInt();
				int b = nextInt();
				graph.get(a).add(b); // 건물 a -> b
				degree[b]++;
			}
			nextLine();
			int W = nextInt(); // 승리하기 위해 건설해야 할 건물 번호
			
			Queue<Integer> q = new LinkedList<>();
			for (int i = 1; i <= N; i++) {
				if (degree[i] == 0) {
					q.add(i);
					answer[i] = time[i];
				}
			}
			while (!q.isEmpty()) {
				int cur = q.poll();
				for (int next : graph.get(cur)) {
					answer[next] = Math.max(answer[next], answer[cur] + time[next]);
					degree[next]--;
					if (degree[next] == 0) q.add(next);
				}
			}
			System.out.println(answer[W]);
		}
	}
}
```
