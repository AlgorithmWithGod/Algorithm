```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

public class Main {
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int t = Integer.parseInt(br.readLine());
		StringBuilder sb = new StringBuilder();
		while (t-- > 0) {
			StringTokenizer st = new StringTokenizer(br.readLine());
			int n = Integer.parseInt(st.nextToken());
			int K = Integer.parseInt(st.nextToken());
			int[] arr = new int[n];
			st = new StringTokenizer(br.readLine());
			for (int i = 0; i < n; i++) {
				arr[i] = Integer.parseInt(st.nextToken());
			}

			Arrays.sort(arr);
			int l = 0;
			int r = n - 1;
			int minDiff = Integer.MAX_VALUE;
			int count = 0;

			while (l < r) {
				int sum = arr[l] + arr[r];
				int diff = Math.abs(K - sum);

				if (diff < minDiff) {
					minDiff = diff;
					count = 1;
				} else if (diff == minDiff) {
					count++;
				}
				if (sum < K) {
					l++;
				} else {
					r--;
				}
			}
			sb.append(count).append("\n");
		}

		System.out.print(sb);
	}
}

```
