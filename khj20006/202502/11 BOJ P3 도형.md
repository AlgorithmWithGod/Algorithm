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
	
	static int[] A;
	static long[][] dp;
	static long[][] sum;
	static int N, K;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
	}
	
	static void ready() throws Exception{

		N = Integer.parseInt(br.readLine());
		A = new int[N];
		nextLine();
		for(int i=0;i<N;i++) A[i] = nextInt();
		K = Integer.parseInt(br.readLine());
		dp = new long[500001][K+1];
		sum = new long[500001][K+1];
		
	}
	
	static void solve() throws Exception{

		Arrays.sort(A);
		dp[A[0]][1] = 1;
		sum[A[0]][1] = 1;
		for(int i=1;i<N;i++) {
			for(int s=500000;s>2*A[i];s--) {
				for(int k=K;k>2;k--) {
					dp[s][k] += sum[s-A[i]][k-1];
				}
			}
			for(int s=500000;s>A[i];s--) {
				for(int k=K;k>1;k--) {
					sum[s][k] += sum[s-A[i]][k-1];
				}
			}
			for(int s=500000;s>A[i];s--) if(dp[s-A[i]][1] != 0) dp[s][2] += dp[s-A[i]][1];
			dp[A[i]][1]++;
			sum[A[i]][1]++;
		}
		
		long ans = 0;
		for(int i=1;i<=500000;i++) ans += dp[i][K];
		bw.write(ans+"\n");
		
	}
	
}

```
