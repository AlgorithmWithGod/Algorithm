```java
import java.io.*;
import java.util.ArrayDeque;
import java.util.Arrays;
import java.util.Queue;
import java.util.StringTokenizer;

public class BJ_28069_김밥천국의_계단 {

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static       StringTokenizer st;

	private static int N, K, nxt;
	private static int[]       minCnt;
	private static Queue<Node> q;

	private static class Node {
		int step;
		int cnt;

		Node(int step, int cnt) {
			this.step = step;
			this.cnt = cnt;
		}
	}

	public static void main(String[] args) throws IOException {
		init();
		sol();

		bw.flush();
		bw.close();
		br.close();
	}

	private static void init() throws IOException {
		st = new StringTokenizer(br.readLine());
		N = Integer.parseInt(st.nextToken());
		K = Integer.parseInt(st.nextToken());

		minCnt = new int[N + 1];
		Arrays.fill(minCnt, Integer.MAX_VALUE);

		q = new ArrayDeque<>();
		q.offer(new Node(0, 0));
		minCnt[0] = 0;
	}

	private static void sol() throws IOException {
		while (!q.isEmpty()) {
			Node cur = q.poll();

			if (cur.step == N) {
				bw.write("minigimbob");
				return;
			}

			if (cur.cnt >= K) {
				continue;
			}

			nxt = cur.step + 1;
			if (nxt <= N && minCnt[nxt] > cur.cnt + 1) {
				minCnt[nxt] = cur.cnt + 1;
				q.offer(new Node(nxt, cur.cnt + 1));
			}

			nxt = cur.step + cur.step / 2;
			if (nxt <= N && minCnt[nxt] > cur.cnt + 1) {
				minCnt[nxt] = cur.cnt + 1;
				q.offer(new Node(nxt, cur.cnt + 1));
			}
		}
		bw.write("water");
	}

}
```