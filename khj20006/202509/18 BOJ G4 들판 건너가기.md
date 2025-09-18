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
	static int[] dp;

	public static void main(String[] args) throws Exception {

		io = new IOController();

		N = io.nextInt()-1;
		
		dp = new int[101];
		Arrays.fill(dp, -1);
		dp[io.nextInt()] = 0;
		
		while(N-->0) {
		    int a = io.nextInt();
		    int max = 0;
		    for(int j=1;j<=100;j++) if(dp[j] != -1) max = Math.max(max, dp[j] + (j-a)*(j-a));
		    dp[a] = Math.max(dp[a], max);
		}
		
		int ans = 0;
		for(int i=1;i<=100;i++) ans = Math.max(ans, dp[i]);
		io.write(ans + "\n");

		io.close();

	}

}
```
