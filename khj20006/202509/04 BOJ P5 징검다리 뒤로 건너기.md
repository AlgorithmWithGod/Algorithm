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

	static final long MOD = (long)1e9 + 7;

	static int N, K;
	static long[][] dp;

	public static void main(String[] args) throws Exception {

		io = new IOController();

		N = io.nextInt();
		K = io.nextInt();
		if(N <= 2) {
			io.write("1\n");
			return;
		}

		dp = new long[N+1][K+1];
		for(int i=3;i<=N;i++) for(int x=1;x<=K && i-x>0;x++) {
			if(i-x <= 2) dp[i][x] = (dp[i][x] + 1) % MOD;
			else for(int y=1;y<=K && i-x-y>0;y++) {
				if(i-x-y <= 2) dp[i][x] = (dp[i][x] + (i-x+1-Math.max(i-x-y+1,i-K))) % MOD;
				else dp[i][x] = (dp[i][x] + dp[i-x][y] * (i-x+1-Math.max(i-x-y+1,i-K))) % MOD;
			}
		}

		long ans = 0;
		for(int x=1;x<=K && N-x>0;x++) ans = (ans + dp[N][x]) % MOD;
		io.write(ans + "\n");

		io.close();

	}

}
```
