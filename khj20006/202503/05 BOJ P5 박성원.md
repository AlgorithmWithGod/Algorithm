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

	static long[][] dp;
	static int N, K;
	static int[] len, A;
	static char[][] temp;
	static long[] pre;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{

		N = Integer.parseInt(br.readLine());
		temp = new char[N][];
		for(int i=0;i<N;i++) temp[i] = br.readLine().toCharArray();
		K = Integer.parseInt(br.readLine());
		dp = new long[K][1<<N];
		len = new int[N];
		A = new int[N];
		pre = new long[16];
		pre[1] = 10;
		for(int i=2;i<16;i++) pre[i] = pre[i-1] * 10;
		
		for(int i=0;i<N;i++) {
			len[i] = temp[i].length;
			int res = 0;
			for(char c : temp[i]) {
				res = (res * 10 + (c-'0')) % K;
			}
			A[i] = res;
			dp[res][1<<i] = 1;
		}
		
	}
	
	static void solve() throws Exception{

		for(int i=1;i<(1<<N);i++) {
			for(int k=0;k<K;k++) {
				for(int x=0;x<N;x++) if((i & (1<<x)) == 0) {
					long tmp = k;
					int cnt = len[x];
					while(cnt > 0) {
						int diff = Math.min(15, cnt);
						tmp = (tmp * pre[diff]) % K;
						cnt-=diff;
					}
					int res = ((int)tmp + A[x]) % K;
					dp[res][i|(1<<x)] += dp[k][i];
				}
			}
		}
		
		long ans = dp[0][(1<<N)-1], total = 1;
		for(long i=2;i<=N;i++) total *= i;
		
		if(ans == 0) total = 1;
		else {
			long[] P = {2,3,5,7,11,13};
			for(long i:P) {
				while(ans%i==0 && total%i==0) {
					ans/=i;
					total/=i;
				}
			}
		}
		bw.write(ans+"/"+total);
		
	}
	
}

```
