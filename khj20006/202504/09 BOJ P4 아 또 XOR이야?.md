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
		while(!st.hasMoreTokens()) nextLine();
		return st.nextToken();
	}
	static int nextInt() throws Exception { return Integer.parseInt(nextToken()); }
	static long nextLong() throws Exception { return Long.parseLong(nextToken()); }
	static double nextDouble() throws Exception { return Double.parseDouble(nextToken()); }
	static void bwEnd() throws Exception {bw.flush();bw.close();}
	
	// Additional field
	
	static long N, A, B;
	static int K;
	static long[][] C;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = nextLong();
		K = nextInt();
		A = nextLong();
		B = nextLong();
		C = new long[62][62];
		C[0][0] = 1;
		for(int i=1;i<=61;i++) {
			C[i][0] = 1;
			for(int j=1;j<i;j++) C[i][j] = C[i-1][j-1] + C[i-1][j];
			C[i][i] = 1;
		}
		
	}
	
	static void solve() throws Exception{
		
		bw.write((f(N,K,B) - f(N,K,A-1)) + "\n");
		
	}
	
	static long f(long n, int k, long x) {
		
		if(x <= 0) return 0L;
		long res = 0, d = 1L;
		int nCount = bits(n);
		int zero = 0, one = 0;
		while((d<<1)-1 <= x) {
			int cur = (n&d) != 0 ? 1 : 0;
			nCount -= cur;
			int temp = k - nCount - (cur^1);
			
			if(temp >= 0) {
				for(int zeroSelect = 0;zeroSelect<=zero;zeroSelect++) {
					int oneSelect = temp - zeroSelect;
					if(oneSelect > one) continue;
					if(oneSelect < 0) break;
					res += C[zero][zeroSelect] * C[one][oneSelect];
				}
			}
			
			if(cur == 0) zero++;
			else one++;
			d<<=1;
		}
		if(x >= d) res += f(n^d, k, x-d) + (bits(n^d) == k ? 1 : 0);
		return res;
		
	}
	
	static int bits(long x) {
		int res = 0;
		for(int i=0;i<=60;i++) res += (x & (1L<<i)) == 0 ? 0 : 1;
		return res;
	}
	
}

```
