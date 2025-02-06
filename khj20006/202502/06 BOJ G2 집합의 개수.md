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
	static int[] cnt;
	static int T, A, S, B;
	static int mod = 1000000;
	
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
		
		bwEnd();
	}
	
	static void ready() throws Exception{

		nextLine();
		T = nextInt();
		A = nextInt();
		S = nextInt();
		B = nextInt();
		dp = new int[A+1];
		cnt = new int[201];
		
		nextLine();
		for(int i=0;i<A;i++) cnt[nextInt()]++;
		
	}
	
	static void solve() throws Exception{
		
		dp[0] = 1;
		
		for(int i=1;i<=200;i++) {
			int[] ndp = new int[A+1];
			ndp[0] = 1;
			
			for(int j=1;j<=A;j++) {
				for(int k=0;k<=Math.min(j, cnt[i]);k++) {
					ndp[j] += dp[j-k];
					ndp[j] %= mod;
				}
			}
			dp = ndp;
		}
		
		int ans = 0;
		for(int j=S;j<=B;j++) ans = (ans + dp[j]) % mod;
		
		bw.write(ans+"\n");
		
	}
	
}

```
