```java
import java.util.*;
import java.io.*;

class IOController {
	BufferedReader br;
	BufferedWriter bw;
	StringTokenizer st;

	public IOController() {
		br = new BufferedReader(new InputStreamReader(System.in));
		bw = new BufferedWriter(new OutputStreamWriter(System.out));
		st = new StringTokenizer("");
	}

	String nextLine() throws Exception {
		String line = br.readLine();
		st = new StringTokenizer(line);
		return line;
	}

	String nextToken() throws Exception {
		while (!st.hasMoreTokens()) nextLine();
		return st.nextToken();
	}

	int nextInt() throws Exception {
		return Integer.parseInt(nextToken());
	}

	long nextLong() throws Exception {
		return Long.parseLong(nextToken());
	}

	double nextDouble() throws Exception {
		return Double.parseDouble(nextToken());
	}

	void close() throws Exception {
		bw.flush();
		bw.close();
	}

	void write(String content) throws Exception {
		bw.write(content);
	}

}

public class Main {

	static IOController io;

	//

	static final int INF = (int)1e9 + 7;

	static int N, W;
	static int[][] arr;

	public static void main(String[] args) throws Exception {

		io = new IOController();

		for(int T=io.nextInt();T-->0;) {
			N = io.nextInt();
			W = io.nextInt();
			arr = new int[N+1][2];
			for(int i=1;i<=N;i++) arr[i][0] = io.nextInt();
			for(int i=1;i<=N;i++) arr[i][1] = io.nextInt();

			int ans = Integer.MAX_VALUE;
			arr[0][0] = arr[0][1] = INF;
			ans = Math.min(ans, get(2));
			arr[0][0] = arr[N][0];
			arr[N][0] = INF;
			ans = Math.min(ans, get(1));
			arr[N][0] = arr[0][0];
			arr[0][0] = INF;
			arr[0][1] = arr[N][1];
			arr[N][1] = INF;
			ans = Math.min(ans, get(0));
			arr[0][0] = arr[N][0];
			arr[N][0] = INF;
			for(int i=N;i>=1;i--) {
				arr[i][0] = arr[i-1][0];
				arr[i][1] = arr[i-1][1];
			}
			arr[0][0] = arr[0][1] = INF;
			ans = Math.min(ans, get(2));
			io.write(ans + "\n");
		}

		io.close();

	}

	static int get(int x) {
		int[][] dp = new int[N+1][3];
		if(x == 1) {
			dp[0][0] = dp[0][2] = 1;
		}
		else if(x == 0) {
			dp[0][1] = dp[0][2] = 1;
		}

		for(int i=1;i<=N;i++) {
			dp[i][0] = dp[i-1][2] + 1;
			if(arr[i-1][0] + arr[i][0] <= W) dp[i][0] = Math.min(dp[i][0], dp[i-1][1] + 1);
			dp[i][1] = dp[i-1][2] + 1;
			if(arr[i-1][1] + arr[i][1] <= W) dp[i][1] = Math.min(dp[i][1], dp[i-1][0] + 1);
			dp[i][2] = dp[i-1][2] + 2;
			if(arr[i-1][0] + arr[i][0] <= W) dp[i][2] = Math.min(dp[i][2], dp[i-1][1] + 2);
			if(arr[i-1][1] + arr[i][1] <= W) dp[i][2] = Math.min(dp[i][2], dp[i-1][0] + 2);
			if(arr[i-1][0] + arr[i][0] <= W && arr[i-1][1] + arr[i][1] <= W) dp[i][2] = Math.min(dp[i][2], dp[i-2][2] + 2);
			if(arr[i][0] + arr[i][1] <= W) dp[i][2] = Math.min(dp[i][2], dp[i-1][2] + 1);
		}
		return dp[N][x];
	}

}
```
