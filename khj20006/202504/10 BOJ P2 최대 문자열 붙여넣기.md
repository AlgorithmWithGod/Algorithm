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
	
	static int M;
	static char[] T;
	static char[][] P;
	static int[][] X;
	static int[] dp;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		T = nextToken().toCharArray();
		dp = new int[T.length];
		M = nextInt();
		P = new char[M][];
		X = new int[M][];
		for(int i=0;i<M;i++) {
			P[i] = nextToken().toCharArray();
			X[i] = new int[P[i].length];
		}
		
	}
	
	static void solve() throws Exception{
		
		for(int i=0;i<M;i++) {
			for(int j=1;j<P[i].length;j++) {
				X[i][j] = X[i][j-1];
				while(X[i][j]>0 && P[i][X[i][j]] != P[i][j]) X[i][j] = X[i][X[i][j]-1];
				if(P[i][X[i][j]] == P[i][j]) X[i][j]++;
			}
		}
		
		int[] idx = new int[M];
		for(int i=0;i<T.length;i++) {
			for(int j=0;j<M;j++) {
				while(idx[j]>0 && P[j][idx[j]] != T[i]) idx[j] = X[j][idx[j]-1];
				if(P[j][idx[j]] == T[i]) idx[j]++;
				if(idx[j] == P[j].length) {
					int res = (i >= P[j].length ? dp[i-P[j].length] : 0) + P[j].length;
					dp[i] = Math.max(dp[i], res);
					idx[j] = X[j][idx[j]-1];
				}
			}
			if(i>0) dp[i] = Math.max(dp[i], dp[i-1]);
		}
		
		bw.write(dp[T.length-1] + "\n");
		
	}
	
}

```
