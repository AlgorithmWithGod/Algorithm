```java
import java.io.*;
import java.util.Arrays;
import java.util.StringTokenizer;

public class BJ_12099_점심메뉴 {

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static final StringBuilder   sb = new StringBuilder();
	private static       StringTokenizer st;

	private static int N;
	private static int Q;

	private static Node[] taste;
	private static int[]  sweetness;

	private static class Node implements Comparable<Node> {
		int spiciness;
		int sweetness;

		Node(int s, int w) {
			spiciness = s;
			sweetness = w;
		}

		@Override
		public int compareTo(Node o) {
			return Integer.compare(this.spiciness, o.spiciness);
		}
	}

	public static void main(String[] args) throws IOException {
		init();
		sol();
	}

	private static void init() throws IOException {
		st = new StringTokenizer(br.readLine());
		N  = Integer.parseInt(st.nextToken());
		Q  = Integer.parseInt(st.nextToken());

		taste = new Node[N];
		for (int i = 0; i < N; i++) {
			st = new StringTokenizer(br.readLine());

			int s = Integer.parseInt(st.nextToken());
			int w = Integer.parseInt(st.nextToken());

			taste[i] = new Node(s, w);
		}

		Arrays.sort(taste);
	}

	private static void sol() throws IOException {
		while (Q-- > 0) {
			st = new StringTokenizer(br.readLine());

			int s1 = Integer.parseInt(st.nextToken());
			int s2 = Integer.parseInt(st.nextToken());
			int w1 = Integer.parseInt(st.nextToken());
			int w2 = Integer.parseInt(st.nextToken());

			int left  = lowerBound(s1);
			int right = upperBound(s2);

			if (left >= right) {
				sb.append("0\n");
				continue;
			}

			int cnt = 0;
			for (int i = left; i < right; i++) {
				if (w1 <= taste[i].sweetness && taste[i].sweetness <= w2) {
					cnt++;
				}
			}
			sb.append(cnt).append("\n");
		}
		bw.write(sb.toString());
		bw.flush();
		bw.close();
		br.close();
	}

	// s1 이상인 첫 번째 인덱스
	private static int lowerBound(int target) {
		int left  = 0;
		int right = N;

		while (left < right) {
			int mid = left + (right - left) / 2;

			if (taste[mid].spiciness < target) {
				left = mid + 1;
			} else {
				right = mid;
			}
		}
		return left;
	}

	// s2 초과인 첫 번째 인덱스
	private static int upperBound(int target) {
		int left  = 0;
		int right = N;

		while (left < right) {
			int mid = left + (right - left) / 2;

			if (taste[mid].spiciness <= target) {
				left = mid + 1;
			} else {
				right = mid;
			}
		}
		return left;
	}

}
```