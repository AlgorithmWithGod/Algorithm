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
	static int[] p;
	static long[] s;
	static int[] r;
	static int[][] par;
	static int[] dep;
	static List<Integer>[] graph;
	static List<int[]> edges;

	static int f(int x) {return x==r[x] ? x : (r[x]=f(r[x]));}

	public static void main(String[] args) throws Exception {

		io = new IOController();

		init();
		solve();

		io.close();

	}

	static void init() throws Exception {

		N = io.nextInt();
		p = new int[N+1];
		s = new long[N+1];
		r = new int[N+1];
		par = new int[N+1][18];
		graph = new List[N+1];
		dep = new int[N+1];
		for(int i=1;i<=N;i++) {
			p[i] = io.nextInt();
			r[i] = i;
			graph[i] = new ArrayList<>();
		}
		edges = new ArrayList<>();
		for(int i=1;i<N;i++) {
			int a = p[io.nextInt()];
			int b = p[io.nextInt()];
			edges.add(new int[]{Math.min(a,b), Math.max(a,b)});
			graph[a].add(b);
			graph[b].add(a);
		}

	}

	static void solve() throws Exception {

		dfs(N,0,0);
		for(int k=1;k<18;k++) for(int i=1;i<=N;i++) par[i][k] = par[par[i][k-1]][k-1];

		Collections.sort(edges, (a,b) -> a[1]==b[1] ? a[0]-b[0] : a[1]-b[1]);
		for(int[] edge : edges) {
			int a = edge[0], b = edge[1];
			int x = f(a), y = f(b);
			s[y] = Math.max(s[y], s[x] + dist(x, y));
			r[x] = y;
		}
		io.write(s[N] + "\n");

	}

	static void dfs(int n, int p, int d) {
		par[n][0] = p;
		dep[n] = d;
		for(int i:graph[n]) if(i != p) dfs(i,n,d+1);
	}

	static int dist(int a, int b) {
		int diff = Math.abs(dep[a]-dep[b]);
		int res = 0;
		for(int k=0;k<18;k++) if((diff & (1<<k)) != 0) {
			if(dep[a] > dep[b]) a = par[a][k];
			else b = par[b][k];
			res += (1<<k);
		}

		for(int k=17;k>=0;k--) if(par[a][k] != par[b][k]) {
			res += (1<<(k+1));
			a = par[a][k];
			b = par[b][k];
		}
		if(a != b) res += 2;
		return res;
	}

}
```
