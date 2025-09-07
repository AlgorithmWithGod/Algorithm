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

	static int N, M;
	static long[][] h, c, s;

	public static void main(String[] args) throws Exception {

		io = new IOController();

		N = io.nextInt();
		M = io.nextInt();
		h = new long[N+1][N+1];
		c = new long[N+1][N+1];
		s = new long[N+1][N+1];
		for(int i=0;i<N;i++) for(int j=0;j<N;j++) h[i][j] = -io.nextLong();

		for(int i=0;i+M<=N;i++) {
			for(int j=0;j+M<=N;j++) {
				long res = h[i][j] - c[i][j];
				s[i+M/2][j+M/2] = res;
				c[i+1][j] += h[i][j];
				c[i][j+1] += h[i][j];
				c[i+1][j+1] -= h[i][j];
				c[i+M][j] -= res;
				c[i][j+M] -= res;
				c[i+M][j+M] += res;
			}
		}

		for(int i=0;i<N;i++) {
			for(int j=0;j<N;j++) io.write(s[i][j] + " ");
			io.write("\n");
		}

		io.close();

	}

}
```
