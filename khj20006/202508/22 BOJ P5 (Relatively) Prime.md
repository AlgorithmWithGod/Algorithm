```java
import java.awt.image.AreaAveragingScaleFilter;
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

	static final long MOD = 998244353;
	static long P, N, M;

	public static void main(String[] args) throws Exception {

		io = new IOController();

		for(int T=io.nextInt(); T-->0; ) {
			init();
			solve();
		}

		io.close();

	}

	static void init() throws Exception {

		P = io.nextLong();
		N = io.nextLong();
		M = io.nextLong();

	}

	static void solve() throws Exception {

		if(N < M) {
			long t = N;
			N = M;
			M = t;
		}

		long pm = power(P, M);
		long ans = pm * ((power(pm, N/M) + MOD - 1) % MOD) % MOD;
		ans = (ans * (power((pm+MOD-1)%MOD, MOD-2))) % MOD;
		if(N%M != 0) ans = (ans + power(P, N)) % MOD;

		if(pm == 1) {
			ans = N/M;
			if(N%M != 0) ans = (ans + power(P, N)) % MOD;
		}
		io.write(ans + "\n");

	}

	static long power(long a, long x) {
		if(x == 0) return 1;
		if(x == 1) return a%MOD;
		long h = power(a, x>>1) % MOD;
		if(x%2 == 0) return h*h%MOD;
		return h*h%MOD*a%MOD;
	}

}
```
