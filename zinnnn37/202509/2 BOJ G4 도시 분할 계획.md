```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.List;
import java.util.PriorityQueue;
import java.util.Queue;
import java.util.StringTokenizer;

public class BJ_1647_도시_분할_계획 {

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static       StringTokenizer st;

	private static int N; // node
	private static int M; // edge
	private static int cnt;
	private static int ans;

	private static int[] parents;

	private static Queue<Node>  pq;
	private static List<Node>[] graph;

	private static class Node implements Comparable<Node> {
		int from;
		int to;
		int weight;

		public Node(int from, int to, int weight) {
			this.from   = from;
			this.to     = to;
			this.weight = weight;
		}

		@Override
		public int compareTo(Node o) {
			return Integer.compare(this.weight, o.weight);
		}
	}

	private static StringTokenizer tokenize() throws IOException {
		return new StringTokenizer(br.readLine());
	}

	private static int nextInt() {
		return Integer.parseInt(st.nextToken());
	}

	public static void main(String[] args) throws IOException {
		init();
		sol();
	}

	private static void init() throws IOException {
		st = tokenize();

		N   = nextInt();
		M   = nextInt();
		cnt = 0;
		ans = 0;

		pq = new PriorityQueue<>();
		while (M-- > 0) {
			st = tokenize();

			int a = nextInt();
			int b = nextInt();
			int c = nextInt();

			pq.add(new Node(a, b, c));
		}

		parents = new int[N + 1];
		for (int i = 1; i <= N; i++) {
			parents[i] = i;
		}
	}

	private static void sol() {
		while (!pq.isEmpty() && cnt < N - 2) {
			Node cur = pq.poll();

			if (find(cur.from) == find(cur.to)) {
				continue;
			}
			union(cur.from, cur.to);
			cnt++;
			ans += cur.weight;
		}
		System.out.println(ans);
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

	private static int find(int a) {
		if (parents[a] == a) {
			return a;
		}
		return parents[a] = find(parents[a]);
	}

}
```