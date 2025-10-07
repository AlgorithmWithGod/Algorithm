```java
import java.io.*;
import java.util.StringTokenizer;

public class BJ_1976_여행_가자 {

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static       StringTokenizer st;

	private static int N, M;
	private static int[] parents;

	public static void main(String[] args) throws IOException {
		init();
		sol();

		bw.flush();
		bw.close();
		br.close();
	}

	private static void init() throws IOException {
		N = Integer.parseInt(br.readLine());
		M = Integer.parseInt(br.readLine());

		parents = new int[N + 1];
		for (int i = 1; i <= N; i++) {
			parents[i] = i;
		}
	}

	private static void sol() throws IOException {
		for (int i = 1; i <= N; i++) {
			st = new StringTokenizer(br.readLine());
			for (int j = 1; j <= N; j++) {
				if (st.nextToken().equals("0")) continue;

				union(i, j);
			}
		}

		st = new StringTokenizer(br.readLine());
		int v = Integer.parseInt(st.nextToken());
		while (M-- > 1) {
			int u = Integer.parseInt(st.nextToken());

			if (find(v) != find(u)) {
				bw.write("NO\n");
				return;
			}
		}
		bw.write("YES\n");
	}

	private static int find(int a) {
		if (parents[a] == a) return a;

		return parents[a] = find(parents[a]);
	}

	private static void union(int a, int b) {
		int rootA = find(a);
		int rootB = find(b);

		if (rootA < rootB) {
			parents[rootB] = rootA;
		} else {
			parents[rootA] = rootB;
		}
	}

}
```