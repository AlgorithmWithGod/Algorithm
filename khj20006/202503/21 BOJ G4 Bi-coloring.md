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
		while(!st.hasMoreTokens()) nextLine();
		return st.nextToken();
	}
	static int nextInt() throws Exception { return Integer.parseInt(nextToken()); }
	static long nextLong() throws Exception { return Long.parseLong(nextToken()); }
	static double nextDouble() throws Exception { return Double.parseDouble(nextToken()); }
	static void bwEnd() throws Exception {bw.flush();bw.close();}
	
	// Additional field
	
	static int N, M;
	static boolean[][] E;
	static int[] C;
	
	public static void main(String[] args) throws Exception {
		for(int T=nextInt();T-->0;) {
			
			ready();
			solve();
		}
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = nextInt();
		M = nextInt();
		E = new boolean[N][N];
		C = new int[N];
		for(int i=0;i<M;i++) {
			int a = nextInt(), b = nextInt();
			E[a][b] = true;
			E[b][a] = true;
		}
		
	}
	
	static void solve() throws Exception{

		int ans = 1;
		for(int i=0;i<N;i++) if(C[i] == 0) {
			C[i] = 1;
			if(dfs(i,1)) ans<<=1;
			else {
				bw.write("-1\n");
				return;
			}
		}
		bw.write(ans + "\n");
		
	}
	
	static boolean dfs(int n, int c) {
		boolean res = true;
		for(int i=0;i<N;i++) if(E[n][i]) {
			if(C[i] == 0) {
				C[i] = c^2;
				res &= dfs(i,c^2);
			}
			else if(C[i] == c) res = false;
		}
		return res;
	}
	
}

```
