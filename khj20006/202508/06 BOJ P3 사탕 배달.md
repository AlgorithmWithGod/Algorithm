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
	static int[] c;
	static List<Integer>[] graph;
	static int[] dep;
	static int[][] par, bit;
	static int[] king;

	public static void main(String[] args) throws Exception {

		io = new IOController();

		init();
		solve();

		io.close();

	}

	static void init() throws Exception {

		N = io.nextInt();
		c = new int[N+1];
		graph = new List[N+1];
		king = new int[6];
		for(int i=1;i<=N;i++) {
			graph[i] = new ArrayList<>();
			c[i] = io.nextInt();
			king[c[i]] = i;
		}

		for(int i=1;i<N;i++) {
			int a = io.nextInt();
			int b = io.nextInt();
			graph[a].add(b);
			graph[b].add(a);
		}

		dep = new int[N+1];
		par = new int[N+1][17];
		bit = new int[N+1][17];

	}

	static void solve() throws Exception {

		dfs(1,0,0);

		for(int k=1;k<17;k++) for(int i=1;i<=N;i++) {
			par[i][k] = par[par[i][k-1]][k-1];
			bit[i][k] = bit[i][k-1] | bit[par[i][k-1]][k-1];
		}

		M = io.nextInt()-1;
		int prev = io.nextInt();
		int temp = io.nextInt();
		io.write(king[temp] == 0 ? "CRY\n" : "PLAY\n");

		while(M-->0) {
			int cur = io.nextInt();
			int tar = io.nextInt();

			int a = prev, b = cur;
			prev = cur;

			int mask = 0;
			int diff = Math.abs(dep[a] - dep[b]);
			for(int k=0;k<17;k++) if((diff & (1<<k)) != 0) {
				if(dep[a] > dep[b]) {
					mask |= bit[a][k];
					a = par[a][k];
				}
				else {
					mask |= bit[b][k];
					b = par[b][k];
				}
			}

			for(int k=16;k>=0;k--) if(par[a][k] != par[b][k]) {
				mask |= bit[a][k] | bit[b][k];
				a = par[a][k];
				b = par[b][k];
			}
			if(a != b) {
				mask |= bit[a][0] | bit[b][0];
				a = par[a][0];
				b = par[b][0];
			}
			mask |= (1<<c[a]);

			if((mask & (1<<tar)) != 0) io.write("PLAY\n");
			else io.write("CRY\n");

		}

	}

	static void dfs(int n, int p, int d) {
		dep[n] = d;
		par[n][0] = p;
		bit[n][0] = (1<<c[n]);
		for(int i:graph[n]) if(i != p) dfs(i,n,d+1);
	}

}
```
