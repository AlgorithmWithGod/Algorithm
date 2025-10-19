```java
import java.io.*;
import java.util.StringTokenizer;

public class BJ_3830_교수님은_기다리지_않는다 {

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static final StringBuilder   sb = new StringBuilder();
	private static       StringTokenizer st;

	private static int N, M;
	private static int[] parent, weight;

	public static void main(String[] args) throws IOException {
		while (init()) {
			sol();
		}
		bw.flush();
		bw.close();
		br.close();
	}

	private static boolean init() throws IOException {
		st = new StringTokenizer(br.readLine());
		N = Integer.parseInt(st.nextToken());
		M = Integer.parseInt(st.nextToken());

		if (N == 0) return false;

		parent = new int[N + 1];
		weight = new int[N + 1];
		for (int i = 1; i <= N; i++) {
			parent[i] = i;
		}

		return true;
	}

	private static void sol() throws IOException {
		while (M-- > 0) {
			st = new StringTokenizer(br.readLine());

			String cmd = st.nextToken();

			if (cmd.equals("!")) {
				int a = Integer.parseInt(st.nextToken());
				int b = Integer.parseInt(st.nextToken());
				int w = Integer.parseInt(st.nextToken());

				union(a, b, w);
			} else if (cmd.equals("?")) {
				int a = Integer.parseInt(st.nextToken());
				int b = Integer.parseInt(st.nextToken());

				if (find(a) == find(b)) {
					bw.write(weight[b] - weight[a] + "\n");
				} else {
					bw.write("UNKNOWN\n");
				}
			}
		}
	}

	private static int find(int a) {
		if (a == parent[a]) return a;

		int root = find(parent[a]);
		weight[a] += weight[parent[a]];
		parent[a] = root;

		return root;
	}

	private static void union(int a, int b, int w) {
		int rootA = find(a);
		int rootB = find(b);

		if (rootA == rootB) {
			return;
		}

		if (rootA < rootB) {
			parent[rootB] = rootA;
			weight[rootB] = weight[a] - weight[b] + w;
		} else {
			parent[rootA] = rootB;
			weight[rootA] = weight[b] - weight[a] - w;
		}
	}

}
```