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

	static final long INF = -(long)1e18 - 7;

	static int N, M;
	static long[] a, b;

	public static void main(String[] args) throws Exception {

		io = new IOController();

		init();
		solve();

		io.close();

	}

	static void init() throws Exception {

		N = io.nextInt();
		M = io.nextInt();
		a = new long[N+1];
		for(int i=1;i<=N;i++) a[i] = a[i-1] + io.nextInt();
		b = new long[N+1];
		for(int i=1;i<=N;i++) b[i] = io.nextInt();

	}

	static void solve() throws Exception {

		long[] success = new long[N+1];
		long[] fail = new long[N+1];
		long[] bonus = new long[N+1];
		Arrays.fill(bonus, INF);

		for(int i=1;i<=N;i++) {
			success[i] = Math.max(bonus[i-1], Math.max(success[i-1], fail[i-1])) + a[i]-a[i-1];
			fail[i] = Math.max(bonus[i-1], Math.max(success[i-1], fail[i-1])) - (a[i]-a[i-1]);
			if(i >= M) bonus[i] = Math.max(fail[i-M], bonus[i-M]) + a[i]-a[i-M] + b[i];
		}

		io.write(Math.max(bonus[N], Math.max(success[N], fail[N])) + "\n");

	}

}
```
