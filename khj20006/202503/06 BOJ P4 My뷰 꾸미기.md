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
	static long ans = 1;
	static long[] fac = new long[600001];
	static final long mod = (long)1e9 + 7;
	
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = Integer.parseInt(br.readLine());
		fac[0] = 1;
		for(int i=1;i<=600000;i++) fac[i] = (fac[i-1] * i) % mod;
		
	}
	
	static void solve() throws Exception{
		
		while(N-- > 0) {
			nextLine();
			int a = nextInt(), b = nextInt();
			ans = (ans * (comb(a+b,a) + mod - 1)) % mod;
		}
		bw.write(ans + "\n");
		
	}
	
	static long comb(int x, int y) {
		
		return fac[x] * power(fac[x-y], mod-2) % mod * power(fac[y], mod-2) % mod;
		
	}
	
	// x^p % mod
	static long power(long x, long p) {
		if(p == 0) return 1;
		if(p == 1) return x % mod;
		long half = power(x,p>>1) % mod;
		half = half * half % mod;
		if(p%2==0) return half;
		return half * x % mod;
	}
	
}

```
