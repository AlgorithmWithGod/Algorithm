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
	
	static int K;
	static int[] A, B;
	
	public static void main(String[] args) throws Exception {
		
		for(int T=nextInt();T-->0;) {
			
			ready();
			solve();
		}
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		K = nextInt();
		A = new int[K];
		B = new int[K];
		for(int i=0;i<K;i++) A[i] = nextInt();
		for(int i=0;i<K;i++) B[i] = nextInt();
		
	}
	
	static void solve() throws Exception{

		int min = 0;
		int[] cntA = new int[100001];
		int[] cntB = new int[100001];
		for(int i=0;i<K;i++) {
			cntA[A[i]]++;
			cntB[B[i]]++;
		}
		for(int i=0;i<=100000;i++) {
			int com = Math.min(cntA[i], cntB[i]); 
			min += com * i;
			min += (Math.max(cntA[i], cntB[i]) - com) * i;
		}
		
		int max = 0;
		for(int i=0;i<K;i++) for(int j=0;j<K;j++) max += Math.min(B[i], A[j]);
		
		bw.write("Minimalni budova obsahuje " + min + " kostek, ");
		bw.write("maximalni " + max + " kostek.\n");
		
	}
	
}

```
