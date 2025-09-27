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
	static long B, D;
	static List<Integer>[] tree;
	static long[] s;
	static long[][] dp;

	public static void main(String[] args) throws Exception {

		io = new IOController();

		N = io.nextInt();
		B = io.nextInt();
		D = io.nextInt();
		tree = new List[N+1];
		s = new long[N+1];
		dp = new long[N+1][35];
		for(int i=1;i<=N;i++) tree[i] = new ArrayList<>();

		for(int i=1;i<N;i++) {
			int a = io.nextInt();
			int b = io.nextInt();
			tree[a].add(b);
			tree[b].add(a);
		}

		dfs(1,0);

		long ans = Long.MAX_VALUE;
		for(int i=0;i<35;i++) {
			ans = Math.min(ans, dp[1][i]);
		}
		io.write(ans + "\n");

		io.close();

	}

	static void dfs(int n, int p) {
		s[n] = 1;
		int children = 0;
		for(int i:tree[n]) if(i != p) {
			dfs(i, n);
			s[n] += s[i];
			children++;
		}
		dp[n][0] = D*(s[n] - 1);
		for(int h=1;h<35;h++) {
			if(children == 0) dp[n][h] = B*((1L<<(h+1)) - 2);
			else {
				List<long[]> tmp = new ArrayList<>();
				for(int i:tree[n]) if(i != p) {
					tmp.add(new long[]{D*s[i] - dp[i][h-1], i});
				}
				Collections.sort(tmp, (a,b) -> Long.compare(b[0],a[0]));
				if(children == 1) {
					dp[n][h] = dp[(int)tmp.get(0)[1]][h-1] + B*((1L<<h)-1);
				}
				else {
					dp[n][h] = dp[(int)tmp.get(0)[1]][h-1] + dp[(int)tmp.get(1)[1]][h-1];
					for(int i=2;i<tmp.size();i++) dp[n][h] += D*s[(int)tmp.get(i)[1]];
				}
			}
			dp[n][h] = Math.min(dp[n][h], D*(s[n]-1) + B*((1L<<(h+1))-2));
		}
	}

}
```
