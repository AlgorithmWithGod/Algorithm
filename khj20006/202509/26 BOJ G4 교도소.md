```java
import java.io.*;
import java.util.*;

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
		while (!st.hasMoreTokens())
			nextLine();
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
	static long[] a;

	public static void main(String[] args) throws Exception {

		io = new IOController();

		N = io.nextInt();
		a = new long[N];
		long s = 0;
		for(int i=0;i<N;i++) {
			a[i] = io.nextInt();
			s += a[i];
		}

		s /= N;
		long ans = 0;
		for(int i=0;i<N*2-1;i++) {
			int cur = i%N, next = (i+1)%N;
			if(a[cur] > s) {
				long diff = a[cur] - s;
				ans += diff;
				a[cur] -= diff;
				a[next] += diff;
			}
		}
		io.write(ans + "\n");

		io.close();

	}

}
```
