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
		if(!st.hasMoreTokens()) nextLine();
		return st.nextToken();
	}
	static int nextInt() throws Exception { return Integer.parseInt(nextToken()); }
	static long nextLong() throws Exception { return Long.parseLong(nextToken()); }
	static double nextDouble() throws Exception { return Double.parseDouble(nextToken()); }
	static void bwEnd() throws Exception {bw.flush();bw.close();}
	
	// Additional field
	
	static int N;
	static int[][] A;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = nextInt();
		A = new int[N][3];
		for(int i=0;i<N;i++) {
			A[i][0] = nextInt();
			A[i][1] = nextInt();
			A[i][2] = i+1;
		}
		
	}
	
	static void solve() throws Exception{

		Arrays.sort(A, (a,b) -> {
			int resA = (10000-a[1])*a[0] + (a[0]+b[0])*a[1];
			int resB = (10000-b[1])*b[0] + (a[0]+b[0])*b[1];
			if(resA > resB) return -1;
			if(resA < resB) return 1;
			return a[2]-b[2];
		});
		for(int[] i:A) bw.write(i[2] + " ");
		
	}
	
}

```
