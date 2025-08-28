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
	static boolean[][] dp;

	public static void main(String[] args) throws Exception {

		io = new IOController();

		N = io.nextInt();
		a = new int[200001];
		for(int i=0;i<N;i++) a[io.nextInt()]++;
		for(int i=1;i<=200000;i++) a[i] += a[i-1];
		dp = new boolean[200001][450];

		for(int i=0;i<=200000;i++) {
			if(a[i] > 1) dp[i][1] = false;
			else dp[i][1] = true;
		}
		for(int t=2;t<450;t++) for(int i=(t-1)*t+t-1;i<=200000;i++) {
			if(a[i] - a[i-1] == 0) dp[i][t] = dp[i-1][t];
			if(dp[i-2*t+1][t-1] && (a[i-t]-a[i-2*t+1] == 0)) dp[i][t] = true;
		}
		for(int t=1;t<450;t++) if(dp[200000][t]) {
			io.write("YES");
			io.close();
			return;
		}
		io.write("NO");

		io.close();

	}

}
```
