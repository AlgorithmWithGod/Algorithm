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

	static int N;
	static int[] a;
	static long[][] dp;

	public static void main(String[] args) throws Exception {

		io = new IOController();

		N = io.nextInt();
		a = new int[N+1];
		for(int i=1;i<=N;i++) a[i] = io.nextInt();

		dp = new long[N+1][4];
		dp[1][0] = a[1];
		for(int j=1;j<4;j++) dp[1][j] = -(long)1e18;

		for(int i=2;i<=N;i++) {
			long xor = 0;
			for(int j=0;j<4;j++) {
				if(i-j-1 < 0) {
					dp[i][j] = -(long)1e18;
					continue;
				}
				xor ^= a[i-j];
				long max = -(long)1e18;
				for(int k=0;k<4;k++) if(k != j) max = Math.max(max, dp[i-j-1][k]);
				dp[i][j] = max + xor;
			}
		}
		long max = 0;
		for(int j=0;j<4;j++) max = Math.max(max, dp[N][j]);
		io.write(max + "\n");

		io.close();

	}

}
```
