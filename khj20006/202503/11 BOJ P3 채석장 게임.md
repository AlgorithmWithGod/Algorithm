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
	static long[] X, M;
	
	static long f(long x) {
		if(x%4 == 0) return x;
		if(x%4 == 1) return 1;
		if(x%4 == 2) return x+1;
		return 0;
	}
	
	public static void main(String[] args) throws Exception {
			
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = Integer.parseInt(br.readLine());
		X = new long[N];
		M = new long[N];
		for(int i=0;i<N;i++) {
			nextLine();
			X[i] = nextLong();
			M[i] = nextLong();
		}
		
	}
	
	static void solve() throws Exception{
		
		long res = 0;
		for(int i=0;i<N;i++) {
			long x = X[i], m = M[i];
			res ^= f(x-1) ^ f(x+m-1);
		}
		bw.write(res==0 ? "cubelover" : "koosaga");
		
	}
	
}

```
