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
	static PriorityQueue<int[]> Q = new PriorityQueue<>((a,b) -> {
		if(a[0] == b[0]) return b[1]-a[1];
		return a[0]-b[0];
	});
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = nextInt();
		int cur = 0;
		for(int i=0;i<N;i++) {
			int len = nextInt();
			char a = nextToken().charAt(0);
			if(a == 'L') len *= -1;
			int next = cur + len;
			Q.offer(new int[] {Math.min(cur, next),1});
			Q.offer(new int[] {Math.max(cur, next),-1});
			cur = next;
		}
		
	}
	
	static void solve() throws Exception{

		int ans = 0, cnt = 0;
		
		int prev = 0;
		while(!Q.isEmpty()) {
			int now = Q.peek()[0];
			if(cnt > 1) ans += now - prev;
			while(!Q.isEmpty() && Q.peek()[0] == now) cnt += Q.poll()[1];
			prev = now;
		}
		bw.write(ans + "\n");
		
	}
	
}

```
