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
	static long K;
	static List<int[]>[] graph;
	static long[] v;
	static PriorityQueue<Long>[] s;
	static int ans = 0;

	public static void main(String[] args) throws Exception {

		io = new IOController();

		init();
		solve();

		io.close();

	}

	static void init() throws Exception {

		N = io.nextInt();
		K = io.nextLong();
		graph = new ArrayList[N+1];
		v = new long[N+1];
		s = new PriorityQueue[N+1];
		for(int i=1;i<=N;i++) {
			graph[i] = new ArrayList<>();
			s[i] = new PriorityQueue<>((a,b) -> Long.compare(b,a));
			s[i].add(0L);
		}
		for(int i=1;i<N;i++) {
			int a = io.nextInt();
			int b = io.nextInt();
			int c = io.nextInt();
			graph[a].add(new int[]{b,c});
			graph[b].add(new int[]{a,c});
		}

	}

	static void solve() throws Exception {

		dfs(1,0);
		io.write(ans + "\n");

	}

	static void dfs(int n, int p) {
		for(int[] e:graph[n]) if(e[0] != p) {
			int i = e[0], x = e[1];
			dfs(i,n);
			if(s[i].size() > s[n].size()) {
				v[i] += x;
				for(long j:s[n]) s[i].add(j+v[n]-v[i]);
				s[n].clear();
				s[n] = s[i];
				v[n] = v[i];
			}
			else {
				for(long j:s[i]) s[n].add(j+x+v[i]-v[n]);
			}
		}
		while(!s[n].isEmpty() && s[n].peek() + v[n] > K) s[n].poll();
		ans = Math.max(ans, s[n].size());
	}

}
```
