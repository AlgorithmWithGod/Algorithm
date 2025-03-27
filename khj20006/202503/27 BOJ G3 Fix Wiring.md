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
	
	static int N;
	static long[] A;
	
	public static void main(String[] args) throws Exception {
			
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = nextInt();
		A = new long[N*(N-1)/2];
		for(int i=0;i<A.length;i++) A[i] = nextLong();
		
	}
	
	static void solve() throws Exception{
		
		Arrays.sort(A);
		long min = 0, max = 0;
		int cntMin = 0, limitMax = 0, passMax = 0;
		for(int i=0;i<A.length;i++) {
			if(cntMin < N-1) {
				cntMin++;
				min += A[i];
			}
			if(passMax == limitMax) {
				passMax = 1;
				limitMax++;
				max += A[i];
			}
			else passMax++;
		}
		bw.write(min + " " + max);
		
	}
	
}

```
