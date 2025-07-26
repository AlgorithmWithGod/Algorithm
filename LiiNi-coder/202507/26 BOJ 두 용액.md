```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

public class Main {

	private static BufferedReader br;
	private static int n;
	private static int[] arr;

	public static void main(String[] args) throws Exception {
		br = new BufferedReader(new InputStreamReader(System.in));

		n = Integer.parseInt(br.readLine());
		arr = new int[n];

		StringTokenizer st = new StringTokenizer(br.readLine());
		for (int i = 0; i < n; i++) {
			arr[i] = Integer.parseInt(st.nextToken());
		}

		Arrays.sort(arr);

		int left = 0;
		int right = n - 1;

		int ansL = arr[left];
		int ansR = arr[right];
		int minGap = Math.abs(ansL + ansR);
		while (left < right) {
			int sum = arr[left] + arr[right];
			if (Math.abs(sum) < minGap) {
				minGap = Math.abs(sum);
				ansL = arr[left];
				ansR = arr[right];
			}
			if (sum < 0) left++;
			else right--;
		}

		System.out.println(ansL + " " + ansR);
	}
}
```
