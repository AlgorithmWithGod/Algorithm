```java
import java.io.*;
import java.util.StringTokenizer;

public class BJ_13244_Tree {

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static final StringBuilder   sb = new StringBuilder();
	private static       StringTokenizer st;

	private static int T, N, M;
	private static int[] parents;

	public static void main(String[] args) throws IOException {
		T = Integer.parseInt(br.readLine());

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
		M = Integer.parseInt(br.readLine());

		parents = new int[N + 1];
		for (int i = 1; i < N + 1; i++) {
			parents[i] = i;
		}
	}

	private static void sol() throws IOException {
		boolean isTree = true;
		for (int i = 0; i < M; i++) {
			st = new StringTokenizer(br.readLine());

			int a = Integer.parseInt(st.nextToken());
			int b = Integer.parseInt(st.nextToken());

			if (!union(a, b)) {
				isTree = false;
			}
		}

		if (M != N - 1) {
			isTree = false;
		}
		sb.append(isTree ? "tree\n" : "graph\n");
	}

	private static int find(int a) {
		if (parents[a] == a) return a;

		return parents[a] = find(parents[a]);
	}

	private static boolean union(int a, int b) {
		int rootA = find(a);
		int rootB = find(b);

		if (rootA == rootB) return false;

		if (rootA < rootB) {
			parents[rootB] = rootA;
		} else {
			parents[rootA] = rootB;
		}
		return true;
	}

}
```