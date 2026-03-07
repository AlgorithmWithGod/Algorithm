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

		while (t-- > 0){
			StringTokenizer st = new StringTokenizer(br.readLine());
			int n = Integer.parseInt(st.nextToken());
			long[] arr = new long[n];

			for(int i = 0; i < n; i++){
				arr[i] = Long.parseLong(st.nextToken());
			}
			Arrays.sort(arr);

			long[] prefix = new long[n + 1];
			for(int i = 1; i <= n; i++) {
				prefix[i] = prefix[i - 1] + arr[i - 1];
			}

			long totalSum = 0;
			for(int k = 2; k <= n; k++){
				long minCost = Long.MAX_VALUE;
				for(int j = k; j <= n; j++){
					long sum = prefix[j] - prefix[j-k];
					long cost = (arr[j-1] * k) - sum;
					if(cost < minCost) {
						minCost = cost;
					}
				}
				totalSum += minCost;
			}
			sb.append(totalSum).append('\n');
		}

		System.out.print(sb);
	}
}
```
