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
	
	static int N, K;
	static int[] A, sum;
	static long[][] dp, S;
	static final long INF = (long)1e18;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = nextInt();
		K = nextInt();
		A = new int[N+1];
		sum = new int[N+1];
		for(int i=1;i<=N;i++) {
			A[i] = nextInt();
			sum[i] = sum[i-1] + A[i];
		}
		dp = new long[N+1][K+1];
		S = new long[N+1][K+1];
		for(int i=0;i<=N;i++) Arrays.fill(dp[i], INF);
		dp[0][0] = 0;
		
	}
	
	static void solve() throws Exception{

		long ans = INF;
		dp[1][1] = 0;
		long temp = 0;
		for(int i=1;i<=N;i++) {
			temp = Math.max(temp, A[i]);
			dp[i][0] = temp*i - sum[i];
		}
		for(int i=2;i<=N;i++) {
			for(int k=1;k<=Math.min(i,K);k++) {
				int max = A[i];
				for(int j=i-1;j>=k;j--) {
					if(dp[j][k-1] == INF) continue;
					dp[i][k] = Math.min(dp[i][k], dp[j][k-1] + (long)max * (i-j) - (sum[i]-sum[j]));
					max = Math.max(max, A[j]);
				}
				if(i == N) ans = Math.min(ans, dp[i][k]);
			}
		}
		bw.write(ans + "\n");
		
	}
	
}

```
