```java
import java.io.*;
import java.util.PriorityQueue;
import java.util.Queue;
import java.util.StringTokenizer;

public class BJ_2696_중앙값_구하기 {

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static       StringTokenizer st;

	private static int    T;
	private static int    M;
	private static String s;

	private static Queue<Integer> minq;
	private static Queue<Integer> maxq;

	public static void main(String[] args) throws IOException {
		sol();
	}

	private static void sol() throws IOException {
		T = Integer.parseInt(br.readLine());

		while (T-- > 0) {
			M = Integer.parseInt(br.readLine());
			bw.write((M / 2 + 1) + "\n");

			s    = "";
			minq = new PriorityQueue<>();
			maxq = new PriorityQueue<>((a, b) -> b - a);
			for (int i = 0; i < M; i++) {
				if (i % 10 == 0) {
					st = new StringTokenizer(br.readLine());
				}

				if (i % 2 == 0) {
					maxq.offer(Integer.parseInt(st.nextToken()));
				} else {
					minq.offer(Integer.parseInt(st.nextToken()));
				}

				if (!minq.isEmpty() && maxq.peek() > minq.peek()) {
					minq.offer(maxq.poll());
					maxq.offer(minq.poll());
				}

				if (i % 2 == 0) {
					bw.write(maxq.peek() + (i > 2 && (i + 2) % 20 == 0 ? "\n" : " "));
				}
			}
			bw.write("\n");
		}
		bw.flush();
		bw.close();
		br.close();
	}

}
```