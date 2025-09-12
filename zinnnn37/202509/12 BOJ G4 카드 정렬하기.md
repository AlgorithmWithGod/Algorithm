```java
import java.io.*;
import java.util.PriorityQueue;
import java.util.Queue;

public class BJ_1715_카드_정렬하기 {

	private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

	private static int N;
	private static int ans;

	private static Queue<Integer> pq;

	public static void main(String[] args) throws IOException {
		init();
		sol();
	}

	private static void init() throws IOException {
		pq  = new PriorityQueue<>();
		ans = 0;

		N = Integer.parseInt(br.readLine());
		while (N-- > 0) {
			int n = Integer.parseInt(br.readLine());
			pq.offer(n);
		}
	}

	private static void sol() throws IOException {
		while (pq.size() > 1) {
			int a = pq.poll();
			int b = pq.poll();

			pq.add(a + b);
			ans += a + b;
		}
		bw.write(ans + "");
		bw.flush();
		bw.close();
		br.close();
	}

}
```