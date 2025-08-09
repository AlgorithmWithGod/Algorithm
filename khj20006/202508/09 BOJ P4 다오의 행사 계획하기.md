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

	static int N, M, T;
	static int[][] row, col;
	static List<Integer>[] graph;
	static int[][] par;
	static int[] dep;
	static long[] arr;

	public static void main(String[] args) throws Exception {

		io = new IOController();

		init();
		solve();

		io.close();

	}

	static void init() throws Exception {

		N = io.nextInt();
		M = io.nextInt();
		T = io.nextInt();
		row = new int[N][M];
		col = new int[N][M];
		for(int i=0;i<N-1;i++) for(int j=0;j<M;j++) row[i][j] = io.nextInt();
		for(int i=0;i<N;i++) for(int j=0;j<M-1;j++) col[i][j] = io.nextInt();
		graph = new List[N*M];
		for(int i=0;i<N*M;i++) graph[i] = new ArrayList<>();
		par = new int[N*M+1][17];
		dep = new int[N*M];
		arr = new long[T+2];

	}

	static void solve() throws Exception {

		for(int i=0;i<N;i++) for(int j=0;j<M;j++) {
			if(i<N-1 && row[i][j] == 0) {
				graph[i*M+j].add((i+1)*M+j);
				graph[(i+1)*M+j].add(i*M+j);
			}
			if(j<M-1 && col[i][j] == 0) {
				graph[i*M+j].add(i*M+j+1);
				graph[i*M+j+1].add(i*M+j);
			}
		}

		dfs(0,N*M,0);
		for(int k=1;k<17;k++) for(int i=0;i<N*M;i++) par[i][k] = par[par[i][k-1]][k-1];

		for(int K=io.nextInt();K-->0;) {
			int s = io.nextInt();
			int e = io.nextInt();
			int a = io.nextInt();
			int b = io.nextInt();
			int c = io.nextInt();
			int d = io.nextInt();
			int v = io.nextInt();

			int x = a*M+b, y = c*M+d;

			int dist = 1, diff = Math.abs(dep[x]-dep[y]);
			for(int k=0;k<17;k++) if((diff & (1<<k)) != 0) {
				if(dep[x] > dep[y]) {
					dist += (1<<k);
					x = par[x][k];
				}
				else {
					dist += (1<<k);
					y = par[y][k];
				}
			}

			for(int k=16;k>=0;k--) if(par[x][k] != par[y][k]) {
				dist += (1<<(k+1));
				x = par[x][k];
				y = par[y][k];
			}
			if(x != y) dist += 2;

			arr[s] += v*dist;
			arr[e+1] -= v*dist;

		}

		long s = 0;
		for(int i=1;i<=T;i++) {
			s += arr[i];
			io.write(s + "\n");
		}

	}

	static void dfs(int n, int p, int d) {
		dep[n] = d;
		par[n][0] = p;
		for(int i:graph[n]) if(i != p) dfs(i,n,d+1);
	}

}
```
