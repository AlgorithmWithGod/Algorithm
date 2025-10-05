```java
import java.io.*;

public class BJ_2133_타일_채우기 {

	private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

	private static int   N;
	private static int[] dp;

	public static void main(String[] args) throws IOException {
		init();
		sol();
	}

	private static void init() throws IOException {
		N  = Integer.parseInt(br.readLine());
		dp = new int[N + 1];

		if (N <= 1) return;

		dp[0] = 1;
		dp[2] = 3;
	}

	private static void sol() throws IOException {
		for (int i = 4; i <= N; i += 2) {
			dp[i] = dp[i - 2] * 4 - dp[i - 4];
		}
		bw.write(dp[N] + "\n");
		bw.flush();
		bw.close();
		br.close();
	}

}
```