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
	
	static int L;
	static char[] A;
	static int[] X;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		L = nextInt();
		X = new int[L];
		A = br.readLine().toCharArray();
		
	}
	
	static void solve() throws Exception{
		
		X[0] = 0;
		for(int i=1;i<L;i++) {
			int j = X[i-1];
			while(j>0 && A[j] != A[i]) j = X[j-1];
			X[i] = j + (A[j] == A[i] ? 1 : 0);
		}
		
		bw.write((L-X[L-1]) + "\n");
		
	}
	
}

```
