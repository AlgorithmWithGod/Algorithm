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
	static int N, L, R, O;
	static long[][] S;
	static long[] sz;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{

		O = Integer.parseInt(br.readLine());
		L = Integer.parseInt(br.readLine());
		R = Integer.parseInt(br.readLine());
		N = Integer.parseInt(br.readLine());
		S = new long[4][N+1];
		sz = new long[N+1];
		sz[0] = 1;
		for(int i=1;i<=N;i++) sz[i] = sz[i-1] * 3;
		
	}
	
	static void solve() throws Exception{

		for(int c=1;c<=3;c++) {
			S[1][0] = c == 1 ? 1 : 0;
			S[2][0] = c == 2 ? 1 : 0;
			S[3][0] = c == 3 ? 1 : 0;
			for(int n=1;n<=N ;n++) {
				S[1][n] = S[1][n-1] + S[3][n-1] + S[2][n-1];
				S[2][n] = S[2][n-1] + S[1][n-1]*2;
				S[3][n] = S[2][n-1]*2 + S[3][n-1];
			}
			bw.write(dnc(O, N, L, R) + " ");
		}
		
	}
	
	
	// S[k][dep]에서 s~e의 합 구하기
	static long dnc(int k, int dep, int s, int e) {
		
		long len = e-s+1;
		if(s>e) return 0;
		if(len == sz[dep]) return S[k][dep];
		
		long m = sz[dep]/3;
		long temp = 0;
		if(k == 1) {
			
			long r = Math.min(m-1, e);
			temp += dnc(1,dep-1,s,(int)r);
			s -= m;
			e -= m;
			r = Math.min(m-1, e);
			temp += dnc(3,dep-1,Math.max(s, 0),(int)r);
			s -= m;
			e -= m;
			r = Math.min(m-1, e);
			temp += dnc(2,dep-1,Math.max(s, 0),(int)r);
			
		}
		else if(k == 2) {
			
			long r = Math.min(m-1, e);
			temp += dnc(2,dep-1,s,(int)r);
			s -= m;
			e -= m;
			r = Math.min(m-1, e);
			temp += dnc(1,dep-1,Math.max(s, 0),(int)r);
			s -= m;
			e -= m;
			r = Math.min(m-1, e);
			temp += dnc(1,dep-1,Math.max(s, 0),(int)r);
			
		}
		else {
			
			long r = Math.min(m-1, e);
			temp += dnc(2,dep-1,s,(int)r);
			s -= m;
			e -= m;
			r = Math.min(m-1, e);
			temp += dnc(3,dep-1,Math.max(s, 0),(int)r);
			s -= m;
			e -= m;
			r = Math.min(m-1, e);
			temp += dnc(2,dep-1,Math.max(s, 0),(int)r);
			
		}
			
		
		return temp;

		
		
	}
	
	
}

```
