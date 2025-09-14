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
	static int[] a, c, r, e;

	static int f(int x) {return x == r[x] ? x : (r[x]=f(r[x]));}

	public static void main(String[] args) throws Exception {

		io = new IOController();

		N = io.nextInt();
		r = new int[1000001];
		e = new int[1000001];
		for(int i=2;i*i<=1000000;i++) if(e[i] == 0) for(int j=i*i;j<=1000000;j+=i) if(e[j] == 0) e[j] = i;
		for(int i=2;i<=1000000;i++) r[i] = i;
		c = new int[1000001];
		a = new int[N];
		for(int i=0;i<N;i++) {
			a[i] = io.nextInt();
			c[a[i]]++;
		}

		for(int i=0;i<N;i++) {
			int t = a[i];
			while(e[t] != 0) {
				int x = f(a[i]), y = f(e[t]);
				if(x != y) {
					c[y] += c[x];
					r[x] = y;
				}
				t /= e[t];
			}
			if(t != 1) {
				int x = f(a[i]), y = f(t);
				if(x != y) {
					c[y] += c[x];
					r[x] = y;
				}
			}
		}

		int ans = 0;
		for(int i=2;i<=1000000;i++) ans = Math.max(ans, c[f(i)]);
		io.write(ans + "\n");

		io.close();

	}

}
```
