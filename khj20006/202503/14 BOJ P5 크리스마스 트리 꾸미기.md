```java

import java.util.*;
import java.io.*;


class Main {
	
	// IO field
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
	static StringTokenizer st = new StringTokenizer("");

	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() throws Exception {
		if(!st.hasMoreTokens()) nextLine();
		return Integer.parseInt(st.nextToken());
	}
	static long nextLong() throws Exception {
		if(!st.hasMoreTokens()) nextLine();
		return Long.parseLong(st.nextToken());
	}
	static void bwEnd() throws Exception {bw.flush();bw.close();}
	
	// Additional field
	
	static int N, L;
	static long[][] dp, sum;
	static final long mod = 100030001L;
	
	public static void main(String[] args) throws Exception {
			
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = nextInt();
		L = nextInt();
		dp = new long[N+1][N+1];
		sum = new long[N+1][N+1];
		
	}
	
	static void solve() throws Exception{
		
		if(L > N) {
			bw.write("0");
			return;
		}
		dp[0][0] = 1;
		for(int i=0;i<=L;i++) sum[0][i] = 1;
		for(int h=1;h<=L;h++) for(int n=1;n<=N;n++) {
			
			for(int k=0;k<n;k++) {
				dp[n][h] += sum[k][h-1] * dp[n-1-k][h-1];
				dp[n][h] += dp[k][h-1] * sum[n-1-k][h-1];
				dp[n][h] -= dp[k][h-1] * dp[n-1-k][h-1];
				dp[n][h] = (dp[n][h] + mod) % mod;
			}
			
			sum[n][h] = (sum[n][h-1] + dp[n][h]) % mod;
		}
		bw.write(dp[N][L] + "\n");
		
	}
	
}

```
