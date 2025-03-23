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
	static int[] dp;
	static int N, K;
	
	public static void main(String[] args) throws Exception {
		
		//ready();
		solve();
	
		bwEnd();
	}
	
	static void ready() throws Exception{

		
	}
	
	static void solve() throws Exception{
		
		nextLine();
		N = nextInt();
		K = nextInt();
		dp = new int[100001];
		Arrays.fill(dp, Integer.MAX_VALUE-1);
		dp[0] = 0;
		nextLine();
		while(N-- > 0) {
			int now = nextInt();
			for(int j=100000;j>now;j--) if(dp[j-now] != 0) dp[j] = Math.min(dp[j-now]+1, dp[j]);
			dp[now] = 1;
		}
		bw.write((dp[K] == Integer.MAX_VALUE-1 ? -1 : dp[K]) + "\n");
		
			
	}
	
}

```
