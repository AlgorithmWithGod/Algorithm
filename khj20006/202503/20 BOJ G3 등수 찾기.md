```java

import java.util.*;
import java.io.*;

class Main {
	
	// IO field
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
	static StringTokenizer st = new StringTokenizer("");

	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static String nextToken() throws Exception {
		if(!st.hasMoreTokens()) nextLine();
		return st.nextToken();
	}
	static int nextInt() throws Exception { return Integer.parseInt(nextToken()); }
	static long nextLong() throws Exception { return Long.parseLong(nextToken()); }
	static double nextDouble() throws Exception { return Double.parseDouble(nextToken()); }
	static void bwEnd() throws Exception {bw.flush();bw.close();}
	
	// Additional field
	
	static int N, M, X;
	static List<Integer>[] V, E;
	static boolean[] vis;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = nextInt();
		M = nextInt();
		X = nextInt();
		V = new List[N+1];
		E = new List[N+1];
		for(int i=1;i<=N;i++) {
			V[i] = new ArrayList<>();
			E[i] = new ArrayList<>();
		}
		for(int i=0;i<M;i++) {
			int a = nextInt(), b = nextInt();
			V[a].add(b);
			E[b].add(a);
		}
		
	}
	
	static void solve() throws Exception{

		vis = new boolean[N+1];
		int max = N - dfs(V,X) + 1;
		int min = dfs(E,X);
		bw.write(min + " " + max);
		
	}
	
	static int dfs(List<Integer>[] G, int n) {
		int res = 0;
		for(int i:G[n]) if(!vis[i]) {
			vis[i] = true;
			res += dfs(G,i);
		}
		return res+1;
	}
	
}

```
