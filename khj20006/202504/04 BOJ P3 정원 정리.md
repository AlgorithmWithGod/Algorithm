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
	static boolean[][] edge;
	static int[] sub;
	static int[][] dp;
	static final int INF = 1234;
	
	public static void main(String[] args) throws Exception {
			
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = nextInt();
		M = nextInt();
		edge = new boolean[N+1][N+1];
		sub = new int[N+1];
		for(int i=1;i<N;i++) {
			int a = nextInt(), b = nextInt();
			edge[a][b] = edge[b][a] = true;
		}
		dp = new int[N+1][];
		
	}
	
	static void solve() throws Exception{
		
		pre(1,0);
		dfs(1,0);
		int ans = dp[1][M];
		for(int i=2;i<=N;i++) if(sub[i] >= M) ans = Math.min(ans, dp[i][M] + 1);
		bw.write(ans + "\n");
		
	}
	
	static void pre(int n, int p) {
		sub[n] = 1;
		for(int i=1;i<=N;i++) if(edge[n][i] && i != p) {
			pre(i,n);
			sub[n] += sub[i];
		}
	}
	
	static void dfs(int n, int p) {
		
		dp[n] = new int[sub[n]+1];
		Arrays.fill(dp[n], INF);
		dp[n][1] = 0;
		dp[n][0] = 1;
		for(int i=1;i<=N;i++) if(edge[n][i] && i != p) {
			dfs(i,n);
			int[] ndp = new int[sub[n]+1];
			Arrays.fill(ndp, INF);
			for(int k=0;k<=sub[i];k++) {
				for(int g=sub[n];g>=k;g--) {
					ndp[g] = Math.min(ndp[g], dp[i][k] + dp[n][g-k]);
				}
			}
			dp[n] = ndp;
		}
		if(n != 1) dp[n][0] = 1;
	}
	
}

```
