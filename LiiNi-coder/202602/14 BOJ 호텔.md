```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		int C = Integer.parseInt(st.nextToken());
		int N = Integer.parseInt(st.nextToken());
		int[] cost = new int[N];
		int[] people = new int[N];
		int maxP = 0;
		for (int i = 0; i < N; i++) {
			st = new StringTokenizer(br.readLine());
			cost[i] = Integer.parseInt(st.nextToken());
			people[i] = Integer.parseInt(st.nextToken());
			if (people[i] > maxP) {
				maxP = people[i];
			}
		}
		int target = C + maxP;
		int[] dp = new int[target + 1];
		int INF = 1_000_000_000;
		for (int i = 1; i <= target; i++) {
			dp[i] = INF;
		}


		dp[0] = 0;
		for (int i = 0; i < N; i++) {
			int p = people[i];
			int c = cost[i];
			for (int j = p; j <= target; j++) {
				if (dp[j - p] + c < dp[j]) {
					dp[j] = dp[j - p] + c;
				}
			}
		}

		int answer = INF;
		for (int i = C; i <= target; i++) {
			if (dp[i] < answer) {
				answer = dp[i];
			}
		}
		System.out.println(answer);
	}
}
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		int C = Integer.parseInt(st.nextToken());
		int N = Integer.parseInt(st.nextToken());
		int[] cost = new int[N];
		int[] people = new int[N];
		int maxP = 0;
		for (int i = 0; i < N; i++) {
			st = new StringTokenizer(br.readLine());
			cost[i] = Integer.parseInt(st.nextToken());
			people[i] = Integer.parseInt(st.nextToken());
			if (people[i] > maxP) {
				maxP = people[i];
			}
		}
		int target = C + maxP;
		int[] dp = new int[target + 1];
		int INF = 1_000_000_000;
		for (int i = 1; i <= target; i++) {
			dp[i] = INF;
		}


		dp[0] = 0;
		for (int i = 0; i < N; i++) {
			int p = people[i];
			int c = cost[i];
			for (int j = p; j <= target; j++) {
				if (dp[j - p] + c < dp[j]) {
					dp[j] = dp[j - p] + c;
				}
			}
		}

		int answer = INF;
		for (int i = C; i <= target; i++) {
			if (dp[i] < answer) {
				answer = dp[i];
			}
		}
		System.out.println(answer);
	}
}

```
