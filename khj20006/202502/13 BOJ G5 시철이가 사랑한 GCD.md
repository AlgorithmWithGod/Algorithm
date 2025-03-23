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
	static long[] A;
	static int N;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
	}
	
	static void ready() throws Exception{
		
		N = Integer.parseInt(br.readLine());
		A = new long[N];
		nextLine();
		for(int i=0;i<N;i++) A[i] = nextLong();

	}
	
	static void solve() throws Exception{

		bw.write(find(0,N-1) + "\n");
		
	}
	
	static long find(int s, int e) {
		if(s == e) return A[s];
		int m=(s+e-1)/2;
		long left = A[s], right = A[e];
		for(int i=s+1;i<=m;i++) left = gcd(left, A[i]);
		for(int i=m+1;i<e;i++) right = gcd(right, A[i]);
		return Math.max(left + find(m+1,e), right + find(s,m));
	}
	
	static long gcd(long a, long b) {
		if(a < b) {
			long temp = a;
			a = b;
			b = temp;
		}
		return a%b!=0 ? gcd(b,a%b) : b;
	}
	
}

```
