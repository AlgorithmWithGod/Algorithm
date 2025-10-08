```java
import java.io.*;
import java.util.StringTokenizer;

public class BJ_9466_텀_프로젝트 {

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static final StringBuilder   sb = new StringBuilder();
	private static       StringTokenizer st;

	private static int N, cnt;
	private static int[]     group;
	private static boolean[] visited, finished;

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
		N = Integer.parseInt(br.readLine());

		cnt      = 0;
		group    = new int[N + 1];
		visited  = new boolean[N + 1];
		finished = new boolean[N + 1];

		st = new StringTokenizer(br.readLine());
		for (int i = 1; i <= N; i++) {
			group[i] = Integer.parseInt(st.nextToken());
		}
	}

	private static void sol() throws IOException {
		for (int i = 1; i <= N; i++) {
			dfs(i);
		}
		sb.append(N - cnt).append("\n");
	}

	private static void dfs(int node) {
		visited[node] = true;

		int next = group[node];

		if (!visited[next]) {
			dfs(next);
		} else if (!finished[next]) {
			while (next != node) {
				cnt++;
				next = group[next];
			}
			cnt++;
		}
		finished[node] = true;
	}

}
```