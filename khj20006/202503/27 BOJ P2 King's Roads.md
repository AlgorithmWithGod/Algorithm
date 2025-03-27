```java

import java.util.*;
import java.io.*;

class Node{
	int s, e;
	long cost;
	Node(int s, int e, long cost){
		this.s = s;
		this.e = e;
		this.cost = cost;
	}
}

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
	static long M;
	static long[] A;
	
	static int[] r;
	
	public static void main(String[] args) throws Exception {
			
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = nextInt();
		M = nextInt();
		A = new long[N];
		r = new int[N];
		for(int i=0;i<N;i++) {
			A[i] = nextLong();
			r[i] = i;
		}
		
	}
	
	static void solve() throws Exception{
		
		if(N == 1) {
			bw.write("0\n");
			return;
		}
		
		Arrays.sort(A);
		int s = 0, e = N-1, cnt = 0;
		long ans = 0;
		while(cnt<N-1 && A[s]+A[e]<M) {
			ans += A[0]+A[s+1];
			cnt++;
			s++;
		}
		while(cnt<N-1) {
			ans += A[s]+A[e]-M;
			cnt++;
			if(A[s]+A[e-1] >= M) e--;
			else s++;
		}
		bw.write(ans + "\n");
		
		
	}
	
}

```
