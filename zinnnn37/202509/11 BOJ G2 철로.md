```java
import java.io.*;
import java.util.Arrays;
import java.util.PriorityQueue;
import java.util.Queue;
import java.util.StringTokenizer;

public class BJ_13334_철로 {

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static       StringTokenizer st;

	private static int n;
	private static int d;
	private static int ans;

	private static Node[]         nodes;
	private static Queue<Integer> q;

	private static class Node implements Comparable<Node> {
		int h;
		int o;

		Node(int h, int o) {
			this.h = h;
			this.o = o;
		}

		@Override
		public int compareTo(Node o) {
			if (this.o == o.o) {
				return Integer.compare(this.h, o.h);
			}
			return Integer.compare(this.o, o.o);
		}

		@Override
		public String toString() {
			return "[h=" + h + ", o=" + o + "]";
		}
	}

	public static void main(String[] args) throws IOException {
		init();
		sol();
	}

	private static void init() throws IOException {
		n     = Integer.parseInt(br.readLine());
		q     = new PriorityQueue<>();
		ans   = 0;
		nodes = new Node[n];

		for (int i = 0; i < n; i++) {
			st = new StringTokenizer(br.readLine());
			int h = Integer.parseInt(st.nextToken());
			int o = Integer.parseInt(st.nextToken());

			if (h > o) {
				nodes[i] = new Node(o, h);
			} else {
				nodes[i] = new Node(h, o);
			}
		}
		d = Integer.parseInt(br.readLine());
		Arrays.sort(nodes);
	}

	private static void sol() throws IOException {
		for (int i = 0; i < n; i++) {
			// 집-회사 거리가 d보다 큼
			if (nodes[i].o - nodes[i].h > d) {
				continue;
			}

			// 시작점 저장
			q.offer(nodes[i].h);

			// 철로 시작점 ~ 회사(도착지) 거리가 d 안쪽인 경우 철로에 포함되는 것
			while (!q.isEmpty() && nodes[i].o - q.peek() > d) {
				q.poll();
			}
			ans = Math.max(ans, q.size());
		}
		bw.write(ans + "");
		bw.flush();
		bw.close();
		br.close();
	}

}
```