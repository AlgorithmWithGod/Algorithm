```java
import java.io.*;
import java.util.*;

public class BJ_23090_난민 {

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static final StringBuilder   sb = new StringBuilder();
	private static       StringTokenizer st;

	private static int N, x, y, prevY;
	private static long           totalDist;
	private static Shelter        newShelter;
	private static Queue<Shelter> maxHeap  = new PriorityQueue<>((a, b) -> Integer.compare(b.y, a.y));
	private static Queue<Shelter> minHeap  = new PriorityQueue<>((a, b) -> Integer.compare(a.y, b.y));
	private static List<Shelter>  shelters = new ArrayList<>();

	private static class Shelter {
		int x;
		int y;

		Shelter(int x, int y) {
			this.x = x;
			this.y = y;
		}
	}

	public static void main(String[] args) throws IOException {
		N = Integer.parseInt(br.readLine());

		while (N-- > 0) {
			init();
			sol();
		}

		bw.write(sb.toString());
		bw.flush();
		bw.close();
		br.close();
	}

	private static void init() throws IOException {
		st = new StringTokenizer(br.readLine());
		x = Integer.parseInt(st.nextToken());
		y = Integer.parseInt(st.nextToken());

		newShelter = new Shelter(x, y);
	}

	private static void sol() {
		if (maxHeap.isEmpty() || newShelter.y <= maxHeap.peek().y) {
			maxHeap.add(newShelter);
		} else {
			minHeap.add(newShelter);
		}

		if (maxHeap.size() > minHeap.size() + 1) {
			minHeap.add(maxHeap.poll());
		} else if (minHeap.size() > maxHeap.size()) {
			maxHeap.add(minHeap.poll());
		}

		int curY = maxHeap.peek().y;

		// 새로 생긴 대피소의 x, y값 더하기
		totalDist += Math.abs(newShelter.x);
		totalDist += Math.abs(newShelter.y - curY);

		// 변화된 만큼만 계산
		int diff       = curY - prevY;
		int lowerCount = maxHeap.size() - 1;
		int upperCount = minHeap.size();

		totalDist += (long) (lowerCount - upperCount) * diff;

		prevY = curY;

		sb.append(curY).append(" ").append(totalDist).append("\n");
	}
}
```