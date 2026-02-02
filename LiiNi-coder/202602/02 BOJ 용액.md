```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int n = Integer.parseInt(br.readLine());
		long[] arr = new long[n];
		StringTokenizer st = new StringTokenizer(br.readLine());
		for (int i = 0; i < n; i++) {
			arr[i] = Long.parseLong(st.nextToken());
		}
		int l = 0;
		int r = n - 1;
		long bestA = arr[l];
		long bestB = arr[r];
		long bestAbs = Math.abs(arr[l] + arr[r]);

		while (l < r) {
			long sum = arr[l] + arr[r];
			long absSum = Math.abs(sum);
			if (absSum < bestAbs) {
				bestAbs = absSum;
				bestA = arr[l];
				bestB = arr[r];
			}
			if (sum > 0) {
				r--;
			} else {
				l++;
			}
		}
		System.out.println(bestA + " " + bestB);
	}
}

```
