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
	static int T, N, PA, PB;
	static long[] A;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		//solve();
	
		bwEnd();
	}
	
	static void ready() throws Exception{
		
		T = Integer.parseInt(br.readLine());
		while(T-- > 0) {
			nextLine();
			N = nextInt();
			PA = nextInt();
			PB = nextInt();
			if(PA > PB) {
				int temp = PA;
				PA = PB;
				PB = temp;
			}
			A = new long[N];
			nextLine();
			for(int i=0;i<N;i++) A[i] = nextInt();
			solve();
		}
		
	}
	
	static void solve() throws Exception{
		
		Arrays.sort(A);
		long ans = 0, res = 0, mid = -1, cnt = 0;
		for(long i:A) {
			if(i-PA < PB-i) {
				ans += (i-PA) * 2;
				res += (i-PA) * 2;
			}
			else if(i-PA == PB-i) {
				ans += (i-PA) * 2;
				mid = i;
				cnt++;
			}
			else{
				ans += (PB-i) * 2;
				res -= (PB-i) * 2;
			}
		}
		if(mid != -1) {
			long res2 = Long.MAX_VALUE;
			for(long i=0;i<=cnt;i++) res2 = Math.min(res2, Math.abs(res+2*(mid-PA)*(2*i-cnt)));
			res = res2;
		}
		res = Math.abs(res);
		bw.write(ans + " " + res + "\n");
	}
	
}

```
