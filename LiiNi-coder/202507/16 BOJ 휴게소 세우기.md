```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;

public class B1477 {
	private static BufferedReader br;
	private static int n;
	private static int l;
	private static int[] positions;
	private static int m;

	public static void main(String[] args) throws IOException {
		br = new BufferedReader(new InputStreamReader(System.in));
		String[] temp = br.readLine().split(" ");
		n = Integer.parseInt(temp[0]);
		m = Integer.parseInt(temp[1]);
		l = Integer.parseInt(temp[2]);

		positions = new int[n + 2];
		String[] line = br.readLine().split(" ");
		for (int i = 0; i < n; i++) {
			positions[i + 1] = Integer.parseInt(line[i]);
		}
		positions[0] = 0;
		positions[n + 1] = l;

		Arrays.sort(positions);

		int left = 1;
		int right = l;
		int answer = 0;

		while (left <= right) {
			int mid = (left + right) / 2;
			if (canBuild(mid)) {
				answer = mid;
				right = mid - 1;
			} else {
				left = mid + 1;
			}
		}

		System.out.println(answer);
	}

	private static boolean canBuild(int maxDist) {
		int needed = 0;
		for (int i = 1; i < positions.length; i++) {
			int dist = positions[i] - positions[i - 1];
			// 해당 구간에서 몇 개의 휴게소가 필요한가?
			if (dist > maxDist) {
				needed += (dist - 1) / maxDist;
			}
		}
		return needed <= m;
	}
}

```
