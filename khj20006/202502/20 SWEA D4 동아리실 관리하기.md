```java

import java.util.*;
import java.io.*;


class Solution {
	
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
	static int[] dp;
	static int N;
	static final int mod = (int)1e9 + 7;
	
	public static void main(String[] args) throws Exception {
		
		int TC;
		TC = Integer.parseInt(br.readLine());
		ready(TC);
	
		bwEnd();
		
	}
	
	static void ready(int TC) throws Exception{

		for(int tc=1;tc<=TC;tc++) {

			// Write Code

			char[] temp = br.readLine().toCharArray();
			N = temp.length;
			A = new int[N+1];
			for(int i=1;i<=N;i++) A[i] = temp[i-1]-'A';
			dp = new int[16];
			
			//
			
			solve(tc);
			
		}
		
	}
	
	static void solve(int tc) throws Exception{

		// Solve part
		for(int x=0;x<16;x++) if((x&1) != 0 && (x&(1<<A[1])) != 0) dp[x] = 1;
		for(int i=2;i<=N;i++) {
			int[] ndp = new int[16];
			for(int x=0;x<16;x++) if((x&(1<<A[i])) != 0) {
				for(int y=0;y<16;y++) if((x & y) != 0) {
					ndp[x] += dp[y];
					ndp[x] %= mod;
				}
			}
			dp = ndp;
		}
		
		int ans = 0;
		for(int i=0;i<16;i++) ans = (ans + dp[i]) % mod;
		
		//
		
		bw.write("#" + tc + " ");
		
		// Output part
		
		bw.write(ans + "\n");
		
		//
		
	}


	
}

```
