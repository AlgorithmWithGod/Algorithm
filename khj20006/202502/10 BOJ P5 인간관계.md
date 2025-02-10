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
	static long[] dp;
	static long[] s;
	static int[] root;
	static int N, M;
	static final long mod = (int)1e9 + 7;
	
	static int f(int x) { return x==root[x] ? x : (root[x]=f(root[x])); }
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
	}
	
	static void ready() throws Exception{

		nextLine();
		N = nextInt();
		M = nextInt();
		dp = new long[N+1];
		s = new long[N+1];
		root = new int[N+1];
		for(int i=1;i<=N;i++) root[i] = i;
		
	}
	
	static void solve() throws Exception{
		
		dp[1] = 1;
		s[1] = 1;
		for(int i=2;i<=N;i++) {
			long[] ndp = new long[N+1];
			ndp[1] = 1;
			ndp[i] = 1;
			for(int j=2;j<i;j++) {
				ndp[j] = (dp[j] * j + dp[j-1]) % mod;
			}
			
			dp = ndp;
			for(int j=1;j<=i;j++) {
				s[i] = (s[i] + dp[j]) % mod;
			}
		}
		
		while(M-- > 0) {
			nextLine();
			int a = nextInt(), b = nextInt();
			int x = f(a), y = f(b);
			if(x != y) {
				N--;
				root[x] = y;
			}
			bw.write(s[N] + "\n");
		}
		
	}
	
}

```
