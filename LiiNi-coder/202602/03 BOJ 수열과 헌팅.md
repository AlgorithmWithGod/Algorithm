```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

public class Main {
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int n = Integer.parseInt(br.readLine());
		long[] ms = new long[n];
		long[] ps = new long[n];
		long[] sortedMs = new long[n];
		long[] sortedPs = new long[n];
		for (int i = 0; i < n; i++) {
			StringTokenizer st = new StringTokenizer(br.readLine());
			long a = Long.parseLong(st.nextToken());
			long b = Long.parseLong(st.nextToken());
			ms[i] = a - b;
			ps[i] = a + b;
			sortedMs[i] = ms[i];
			sortedPs[i] = ps[i];
		}
		Arrays.sort(sortedMs);
		Arrays.sort(sortedPs);

		StringBuilder sb = new StringBuilder();
		for (int i = 0; i < n; i++) {
			long low = ms[i];
			long high = ps[i];

			int minIdx = lowerBound(sortedPs, low) + 1;
			int maxIdx = upperBound(sortedMs, high);
			sb.append(minIdx).append(" ").append(maxIdx).append("\n");
		}
		System.out.println(sb.toString());
	}

	private static int lowerBound(long[] arr, long target) {
		int l = 0;
		int r = arr.length;
		while (l < r) {
			int mid = (l + r) / 2;
			if (arr[mid] < target) {
				l = mid + 1;
			} else {
				r = mid;
			}
		}
		return l;
	}

	private static int upperBound(long[] arr, long target) {
		int l = 0;
		int r = arr.length;
		while (l < r) {
			int mid = (l + r) / 2;
			if (arr[mid] <= target) {
				l = mid + 1;
			} else {
				r = mid;
			}
		}
		return l;
	}
}

```
