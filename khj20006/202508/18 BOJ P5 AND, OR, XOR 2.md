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

	static int N;
	static int[] a;

	public static void main(String[] args) throws Exception {

		io = new IOController();

		init();
		solve();

		io.close();

	}

	static void init() throws Exception {

		N = io.nextInt();
		a = new int[N+1];
		for(int i=1;i<=N;i++) a[i] = io.nextInt();

	}

	static void solve() throws Exception {

		io.write(and() + " " + or() + " " + xor());

	}

	static long and() {
		long res = 0;
		for(int k=0;k<30;k++) {
			for(int i=1;i<=N;) if((a[i] & (1<<k)) != 0) {
				int j = i;
				while(j<=N && (a[j] & (1<<k)) != 0) j++;
				long cnt = j-i;
				res = (res + ((cnt*(cnt+1)/2)%MOD) * (1<<k)%MOD) % MOD;
				i = j;
			}
			else i++;
		}
		return res;
	}

	static long or() {
		long res = 0;
		for(int k=0;k<30;k++) {
			long coef = (long)N*(N+1)/2;
			for(int i=1;i<=N;) if((a[i] & (1<<k)) == 0) {
				int j = i;
				while(j<=N && (a[j] & (1<<k)) == 0) j++;
				long cnt = j-i;
				coef -= cnt*(cnt+1)/2;
				i = j;
			}
			else i++;
			res = (res + coef%MOD * (1<<k)%MOD) % MOD;
		}
		return res;
	}

	static long xor() {
		long res = 0;
		for(int k=0;k<30;k++) {
			int[] c = new int[N+1];
			long odd = 0, even = 0;
			for(int i=1;i<=N;i++) {
				c[i] += c[i-1];
				if((a[i] & (1<<k)) != 0) c[i]++;
				if(c[i]%2 == 0) {
					if(c[i] > 0) even++;
				}
				else odd++;
			}
			for(int i=1;i<=N;i++) {
				if(c[i-1]%2 == 0) res += odd*(1<<k);
				else res += even*(1<<k);
				res %= MOD;
				if(c[i]%2 == 0) {
					if(c[i] > 0) even--;
				}
				else odd--;
			}
		}
		return res;
	}

}
```
