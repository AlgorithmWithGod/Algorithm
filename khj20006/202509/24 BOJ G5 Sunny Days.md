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
	static int[] a, l, r;

	public static void main(String[] args) throws Exception {

		io = new IOController();

		N = io.nextInt();
		a = new int[N+2];
		for(int i=1;i<=N;i++) a[i] = io.nextToken().equals("S") ? 1 : 0;

		l = new int[N+2];
		for(int i=1;i<=N;i++) l[i] = a[i] == 1 ? l[i-1] + 1 : 0;
		r = new int[N+2];
		for(int i=N;i>=1;i--) r[i] = a[i] == 1 ? r[i+1] + 1 : 0;

		int ans = 0;
		for(int i=1;i<=N;i++) {
			if(a[i] == 0) ans = Math.max(ans, l[i-1] + r[i+1] + 1);
			else ans = Math.max(ans, Math.max(l[i-1], r[i+1]));
		}
		io.write(ans + "\n");

		io.close();

	}

}
```
