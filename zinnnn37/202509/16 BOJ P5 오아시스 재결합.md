```java
import java.io.*;
import java.util.Stack;

public class BJ_3015_오아시스_재결합 {

	private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

	private static int  N;
	private static long ans;

	private static Stack<Node> s;

	private static class Node {
		int val;
		int cnt;

		Node(int val, int cnt) {
			this.val = val;
			this.cnt = cnt;
		}
	}

	public static void main(String[] args) throws IOException {
		sol();
	}

	private static void sol() throws IOException {
		N = Integer.parseInt(br.readLine());
		s = new Stack<>();

		ans = 0;
		for (int i = 0; i < N; i++) {
			int  n   = Integer.parseInt(br.readLine());
			Node cur = new Node(n, 1);

			while (!s.isEmpty() && s.peek().val <= cur.val) {
				Node prev = s.pop();

				ans += prev.cnt;
				if (prev.val == cur.val) {
					cur.cnt += prev.cnt;
				}
			}
			if (!s.isEmpty()) {
				ans++;
			}
			s.push(cur);
		}
		bw.write(ans + "\n");
		bw.flush();
		bw.close();
		br.close();
	}

}
```