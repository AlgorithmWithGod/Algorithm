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
	
	static int N, K, ans = 0;
	static PriorityQueue<Integer> Q;
	
	public static void main(String[] args) throws Exception {
			
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = nextInt();
		K = nextInt();
		Q = new PriorityQueue<>();
		int prev = nextInt(), now = 0;
		
		for(int i=1;i<N;i++) {
			now = nextInt();
			Q.offer(now-prev-1);
			prev = now;
		}
		
	}
	
	static void solve() throws Exception{
		
		ans = N;
		for(int i=N;i>K;i--) ans += Q.poll();
		bw.write(ans + "\n");
		
	}
	
}

```
