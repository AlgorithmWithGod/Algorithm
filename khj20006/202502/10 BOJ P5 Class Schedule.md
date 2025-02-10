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
	static int[][] E, P;
	static int C, T, L;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		//solve();
	
		bwEnd();
	}
	
	static void ready() throws Exception{

		int Z = Integer.parseInt(br.readLine());
		while(Z-- > 0) {
			nextLine();
			C = nextInt();
			T = nextInt();
			L = nextInt();
			dp = new int[T];
			E = new int[C][T];
			P = new int[C][T];
			for(int i=0;i<C;i++) {
				for(int j=0;j<T;j++) {
					nextLine();
					P[i][j] = nextInt();
					E[i][j] = nextInt();
				}
			}
			
			solve();
		}
		
	}
	
	static void solve() throws Exception{

		for(int j=0;j<T;j++) dp[j] = P[0][j] + E[0][j];
		
		for(int i=1;i<C;i++) {
			int[] ndp = new int[T];
			Arrays.fill(ndp, Integer.MAX_VALUE);
			for(int j=0;j<T;j++) {
				for(int k=0;k<T;k++) {
					ndp[j] = Math.min(ndp[j], dp[k] + E[i][j] + Math.abs(P[i][j] - P[i-1][k]));
				}
			}
			dp = ndp;
		}
		
		int ans = Integer.MAX_VALUE;
		for(int j=0;j<T;j++) ans = Math.min(ans, dp[j] + Math.abs(L-P[C-1][j]));
		bw.write(ans+"\n");
		
	}
	
}

```
