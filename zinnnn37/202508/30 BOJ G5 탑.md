```java
import java.io.*;
import java.util.Stack;
import java.util.StringTokenizer;

public class BJ_2493_탑 {

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static final StringBuilder   sb = new StringBuilder();
	private static       StringTokenizer st;

	private static int   N;
	private static int[] height;

	private static Stack<Integer> s;

	public static void main(String[] args) throws IOException {
		init();
		sol();
	}

	private static void init() throws IOException {
		N = Integer.parseInt(br.readLine());

		height = new int[N];
		st     = new StringTokenizer(br.readLine());
		for (int i = 0; i < N; i++) {
			height[i] = Integer.parseInt(st.nextToken());
		}

		s = new Stack<>();
		s.push(0);
		sb.append("0 ");

		br.close();
	}

	private static void sol() throws IOException {
		for (int i = 1; i < N; i++) {
			// 현재 건물보다 높이가 높은 건물이 나올 때 까지 pop
			while (!s.isEmpty() && height[s.peek()] < height[i]) {
				s.pop();
			}

			// 왼쪽에 현재 건물보다 높은 건물 부재
			if (s.isEmpty()) {
				sb.append("0 ");
			} else {
				sb.append(s.peek() + 1).append(" ");
			}
			s.push(i);
		}
		bw.write(sb.toString());
		bw.flush();
		bw.close();
	}

}
```