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

	static long[] C = new long[1000001];
	static long[] ans;
	static List<Integer> A = new ArrayList<>();
	static int N;
	static long[] F = new long[1000001];
	
	static final long mod = 998244353;
	
	public static void main(String[] args) throws Exception {
			
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		
		N = Integer.parseInt(br.readLine());
		for(int p=0;p<N;p++) {
			nextLine();
			for(int i=nextInt();i-->0;) A.add(nextInt());
		}
		Collections.sort(A);
		for(int i=0;i<A.size();) {
			int cnt = 0, a = A.get(i);
			while(i<A.size() && A.get(i).equals(a)) {
				cnt++;
				i++;
			}
			C[cnt]++;
		}
		
		ans = new long[N+1];

		F[0] = 1;
		for(int i=1;i<=N;i++) F[i] = (F[i-1] * i) % mod;
		
	}
	
	static void solve() throws Exception{
		
		for(int i=1;i<=N;i++) if(C[i] > 0) {
			for(int k=1;k<=i;k++) {
				ans[k] = (ans[k] + C[i] * comb(i, k)) % mod;
			}			
		}
		
		for(int i=1;i<=N;i++) bw.write(ans[i] + "\n");
		
	}
	
	static long comb(int n, int k) {
		return F[n] * power(F[k],mod-2) % mod * power(F[n-k],mod-2) % mod;
	}
	
	static long power(long n, long m) {
		if(m == 0) return 1;
		if(m == 1) return n;
		long p = power(n,m>>1) % mod;
		p = (p*p) % mod;
		if(m%2 == 0) return p;
		return p*n%mod;
	}
	
}

```
