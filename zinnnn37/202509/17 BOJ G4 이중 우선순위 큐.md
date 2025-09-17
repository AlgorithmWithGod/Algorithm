```java
import java.io.*;
import java.util.*;

public class BJ_7662_이중_우선순위_큐 {

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static final StringBuilder   sb = new StringBuilder();
	private static       StringTokenizer st;

	private static int N;

	private static PriorityQueue<Integer> minHeap = new PriorityQueue<>();
	private static PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
	private static Map<Integer, Integer>  count   = new HashMap<>();

	public static void main(String[] args) throws IOException {
		int T = Integer.parseInt(br.readLine());

		while (T-- > 0) {
			solve();
		}

		bw.write(sb.toString());
		bw.flush();
		bw.close();
		br.close();
	}

	private static void solve() throws IOException {
		N = Integer.parseInt(br.readLine());

		clear();

		for (int i = 0; i < N; i++) {
			st = new StringTokenizer(br.readLine());

			String command = st.nextToken();
			int    value   = Integer.parseInt(st.nextToken());

			if (command.equals("I")) {
				insert(value);
			} else {
				delete(value == 1 ? maxHeap : minHeap);
			}
		}

		printResult();
	}

	private static void insert(int value) {
		minHeap.offer(value);
		maxHeap.offer(value);
		count.put(value, count.getOrDefault(value, 0) + 1);
	}

	private static void delete(Queue<Integer> heap) {
		while (!heap.isEmpty()) {
			int current      = heap.poll();
			int currentCount = count.getOrDefault(current, 0);

			if (currentCount == 0) continue;

			if (currentCount == 1) {
				count.remove(current);
			} else {
				count.put(current, currentCount - 1);
			}
			break;
		}
	}

	private static void printResult() {
		if (count.isEmpty()) {
			sb.append("EMPTY\n");
			return;
		}

		cleanHeap(maxHeap);
		cleanHeap(minHeap);

		int max = maxHeap.poll();
		int min = minHeap.poll();

		sb.append(max).append(" ").append(min).append("\n");
	}

	private static void cleanHeap(Queue<Integer> heap) {
		while (!heap.isEmpty() && count.getOrDefault(heap.peek(), 0) == 0) {
			heap.poll();
		}
	}

	private static void clear() {
		minHeap.clear();
		maxHeap.clear();
		count.clear();
	}
}
```