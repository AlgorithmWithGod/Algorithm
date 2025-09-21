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

	static int N, M;
	static long[] c;
	static int[] r;

	static int f(int x) {return x==r[x] ? x : (r[x]=f(r[x]));}

	public static void main(String[] args) throws Exception {

		io = new IOController();

		N = io.nextInt();
		M = io.nextInt();
		r = new int[N+1];
		c = new long[N+1];
		for(int i=1;i<=N;i++) {
			c[i] = io.nextLong();
			r[i] = i;
		}

		while(M-->0) {
			int x = f(io.nextInt());
			int y = f(io.nextInt());
			if(x != y) {
				c[y] += c[x];
				r[x] = y;
			}
			io.write(c[y] + "\n");
		}

		io.close();

	}

}
```
