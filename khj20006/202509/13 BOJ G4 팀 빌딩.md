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
	static int[] min, max;

	public static void main(String[] args) throws Exception {

		io = new IOController();

		N = io.nextInt();
		min = new int[10001];
		max = new int[10001];
		for(int i=1;i<=N;i++) {
			int a = io.nextInt();
			if(min[a] == 0) min[a] = i;
			max[a] = i;
		}

		int ans = 0;
		for(int i=1;i<=10000;i++) for(int j=1;j<=10000;j++) {
			if(max[i] == 0 || max[j] == 0 || max[j] == min[i]) continue;
			ans = Math.max(ans, Math.min(i,j) * (max[j] - min[i] - 1));
		}

		io.write(ans + "\n");

		io.close();

	}

}
```
