```java
import java.io.*;
import java.util.*;

public class BJ_1005_ACM_Craft {

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static final StringBuilder   sb = new StringBuilder();
	private static       StringTokenizer st;

	private static int   N;
	private static int   K;
	private static int   W;
	private static int[] dp;
	private static int[] time;
	private static int[] inDegree;

	private static Queue<Integer>  q;
	private static List<Integer>[] graph;

	public static void main(String[] args) throws IOException {
		int T = Integer.parseInt(br.readLine());

		while (T-- > 0) {
			init();
			sol();
		}
		bw.write(sb.toString());
		bw.flush();
		bw.close();
		br.close();
	}

	private static void init() throws IOException {
		st = new StringTokenizer(br.readLine());
		N  = Integer.parseInt(st.nextToken());
		K  = Integer.parseInt(st.nextToken());

		dp   = new int[N + 1];
		time = new int[N + 1];
		st   = new StringTokenizer(br.readLine());
		for (int i = 1; i <= N; i++) {
			time[i] = Integer.parseInt(st.nextToken());
		}

		graph = new ArrayList[N + 1];
		for (int i = 1; i <= N; i++) {
			graph[i] = new ArrayList<>();
		}

		inDegree = new int[N + 1];
		for (int i = 1; i <= K; i++) {
			st = new StringTokenizer(br.readLine());
			int u = Integer.parseInt(st.nextToken());
			int v = Integer.parseInt(st.nextToken());

			graph[u].add(v);
			inDegree[v]++;
		}

		W = Integer.parseInt(br.readLine());
		q = new ArrayDeque<>();
	}

	private static void sol() throws IOException {
		for (int i = 1; i <= N; i++) {
			// 시작 건물
			if (inDegree[i] == 0) {
				dp[i] = time[i];
				q.offer(i);
			}
		}

		while (!q.isEmpty()) {
			int cur = q.poll();

			for (int nxt : graph[cur]) {
				dp[nxt] = Math.max(dp[nxt], dp[cur] + time[nxt]);
				if (--inDegree[nxt] == 0) {
					q.offer(nxt);
				}
			}
		}
		sb.append(dp[W]).append("\n");
	}

}
```