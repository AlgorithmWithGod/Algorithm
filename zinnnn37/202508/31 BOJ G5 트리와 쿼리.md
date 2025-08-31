```java
import java.io.*;
import java.util.ArrayList;
import java.util.List;
import java.util.StringTokenizer;

public class BJ_15681_트리와_쿼리 {

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static final StringBuilder   sb = new StringBuilder();
	private static       StringTokenizer st;

	private static int N;
	private static int R;
	private static int Q;

	private static int[]           dp;
	private static boolean[]       visited;
	private static List<Integer>[] tree;

	public static void main(String[] args) throws IOException {
		init();
		sol();
	}

	private static void init() throws IOException {
		st = new StringTokenizer(br.readLine());

		N = Integer.parseInt(st.nextToken());
		R = Integer.parseInt(st.nextToken());
		Q = Integer.parseInt(st.nextToken());

		tree = new List[N + 1];
		for (int i = 1; i <= N; i++) {
			tree[i] = new ArrayList<>();
		}

		for (int i = 0; i < N - 1; i++) {
			st = new StringTokenizer(br.readLine());
			int u = Integer.parseInt(st.nextToken());
			int v = Integer.parseInt(st.nextToken());

			tree[u].add(v);
			tree[v].add(u);
		}
		visited = new boolean[N + 1];
		dp      = new int[N + 1];
	}

	private static void sol() throws IOException {
		dp[R] = makeDP(R);

		for (int i = 0; i < Q; i++) {
			int q = Integer.parseInt(br.readLine());

			sb.append(dp[q]).append("\n");
		}
		bw.write(sb.toString());
		bw.flush();
		bw.close();
		br.close();
	}

	private static int makeDP(int parent) {
		if (dp[parent] != 0) return dp[parent];

		int cnt = 1;
		for (int i = 0; i < tree[parent].size(); i++) {
			int child = tree[parent].get(i);

			if (visited[child] || child == R) {
				continue;
			}

			visited[child] = true;
			dp[child]      = makeDP(child);
			cnt += dp[child];
		}
		return cnt;
	}

}
```