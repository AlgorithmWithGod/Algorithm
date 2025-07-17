```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;

public class B2110 {
	private static BufferedReader br;
	private static int n;
	private static int c;
	private static int[] houses;

	public static void main(String[] args) throws IOException {
		br = new BufferedReader(new InputStreamReader(System.in));
		String[] temp = br.readLine().split(" ");
		n = Integer.parseInt(temp[0]);
		c = Integer.parseInt(temp[1]);

		houses = new int[n];
		for (int i = 0; i < n; i++) {
			houses[i] = Integer.parseInt(br.readLine());
		}

		Arrays.sort(houses);

		int left = 1;
		int right = houses[n - 1] - houses[0];
		int answer = 0;

		while (left <= right) {
			int mid = (left + right) / 2;
			if (canInstall(mid)) {
				answer = mid;
				left = mid + 1;
			} else {
				right = mid - 1;
			}
		}

		System.out.println(answer);
	}

	private static boolean canInstall(int minDist) {
		int count = 1;
		int lastInstalled = houses[0];
		for (int i = 1; i < n; i++) {
			if (houses[i] - lastInstalled >= minDist) {
				count++;
				lastInstalled = houses[i];
			}
		}
		return count >= c;
	}
}
```
