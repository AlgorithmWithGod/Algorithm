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
	static int N;
	static long mod = (long)1e9 + 9;
	static long[] dp;
	static int[] G = {1,2,1,-1,-2,-1};
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
	}
	
	static void ready() throws Exception{
		
		N = Integer.parseInt(br.readLine());
		dp = new long[N+1];
		
	}
	
	static void solve() throws Exception{
		
		dp[1] = 1;
		for(int i=2;i<=N;i++) dp[i] = (dp[i-1]*3 + dp[i-2] + G[i%6]) % mod;
		bw.write(dp[N] +"\n");
		
	}
	
}

```
