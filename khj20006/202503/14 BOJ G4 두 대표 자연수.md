```java

import java.util.*;
import java.io.*;

class Main {
	
	// IO field
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
	static StringTokenizer st = new StringTokenizer("");

	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() throws Exception {
		if(!st.hasMoreTokens()) nextLine();
		return Integer.parseInt(st.nextToken());
	}
	static long nextLong() throws Exception {
		if(!st.hasMoreTokens()) nextLine();
		return Long.parseLong(st.nextToken());
	}
	static void bwEnd() throws Exception {bw.flush();bw.close();}
	
	// Additional field
	
	static int N;
	static long[] C;
	
	public static void main(String[] args) throws Exception {
			
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = nextInt();
		C = new long[10001];
		for(int i=0;i<N;i++) C[nextInt()]++;
		
	}
	
	static void solve() throws Exception{
		
		long ans1 = -1, res = Long.MAX_VALUE;
		long ans2 = -1, res2 = Long.MAX_VALUE;
		for(int i=1;i<=10000;i++) {
			long temp1 = 0, temp2 = 0;
			for(int j=1;j<=10000;j++) {
				temp1 += C[j] * Math.abs(i-j);
				temp2 += C[j] * (i-j) * (i-j);
			}
			if(temp1 < res) {
				res = temp1;
				ans1 = i;
			}
			if(temp2 < res2) {
				res2 = temp2;
				ans2 = i;
			}
		}
		bw.write(ans1 + " " + ans2);
		
		
	}
	
}

```
