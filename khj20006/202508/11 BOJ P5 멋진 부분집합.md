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

	public static void main(String[] args) throws Exception {

		io = new IOController();

		init();
		solve();

		io.close();

	}

	static void init() throws Exception {

		N = io.nextInt();
		a = new int[N];
		for(int i=0;i<N;i++) a[i] = io.nextInt();

	}

	static void solve() throws Exception {

		for(int t=0;t<50;t++) {
			int idx = (int)(Math.random() * N);
			List<Integer> primes = new ArrayList<>();
			int A = a[idx];
			for(int i=2;i*i<=A;i++) if(A%i == 0) {
				primes.add(i);
				while(A%i == 0) A /= i;
			}
			if(A != 1) primes.add(A);

			for(int p:primes) {
				int cnt = 0;
				for(int i=0;i<N;i++) cnt += (a[i] % p == 0) ? 1 : 0;
				if(cnt >= (N+1)/2) {
					io.write("YES\n");
					int c = 0;
					for(int j=0;j<N;j++) if(a[j] % p == 0) {
						c++;
						io.write(a[j] + " ");
						if(c == (N+1)/2) return;
					}
				}
			}
		}
		io.write("NO");

	}

}
```
