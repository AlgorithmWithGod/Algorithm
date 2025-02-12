```java

import java.util.*;
import java.io.*;

class Main {
	
	// IO field
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
	static StringTokenizer st;

	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	static long nextLong() {return Long.parseLong(st.nextToken());}
	static void bwEnd() throws Exception {bw.flush();bw.close();}
	
	// Additional field
	static int[][] dp;
	static int[] A, B;
	static int N;
	static final int INF = (int)1e9 + 1;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
	}
	
	static void ready() throws Exception{

		N = Integer.parseInt(br.readLine());
		A = new int[N+1];
		B = new int[N+1];
		dp = new int[N+2][N+2];
		for(int i=0;i<N+2;i++) Arrays.fill(dp[i], INF);
		
		nextLine();
		for(int i=1;i<=N;i++) A[i] = nextInt();
		nextLine();
		for(int i=1;i<=N;i++) B[i] = nextInt();
		
	}
	
	static void solve() throws Exception{
		
		dp[0][0] = 0;
		for(int i=1;i<=N+1;i++) for(int j=1;j<=N+1;j++) {
			if(dp[i-1][j] != INF) {
				if(dp[i][j] == INF) dp[i][j] = dp[i-1][j];
				else dp[i][j] = Math.max(dp[i][j], dp[i-1][j]);
			}
			if(dp[i-1][j-1] != INF) {
				if(dp[i][j] == INF) dp[i][j] = dp[i-1][j-1];
				else dp[i][j] = Math.max(dp[i][j], dp[i-1][j-1]);
			}
			if(i<=N && j>1 && A[i] > B[j-1] && dp[i][j-1] != INF) {
				if(dp[i][j] == INF) dp[i][j] = dp[i][j-1] + B[j-1];
				else dp[i][j] = Math.max(dp[i][j], dp[i][j-1] + B[j-1]);
			}
		}
		int ans = 0;
		for(int i=1;i<=N+1;i++) {
			if(dp[i][N+1] != INF) ans = Math.max(ans, dp[i][N+1]);
			if(dp[N+1][i] != INF) ans = Math.max(ans, dp[N+1][i]);
		}
		bw.write(ans+"\n");
		
			
	}
	
}

```
