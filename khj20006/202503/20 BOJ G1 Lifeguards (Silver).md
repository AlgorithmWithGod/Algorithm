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
		for(int i=0;i<N;i++) {
			int a = nextInt(), b = nextInt();
			Q.offer(new int[] {a,1,i});
			Q.offer(new int[] {b,-1,i});
		}
		
	}
	
	static void solve() throws Exception{

		int tot = 0;
		int[] len = new int[N];
		int pos = 0;
		TreeSet<Integer> T = new TreeSet<>();
		while(!Q.isEmpty()) {
			int prev = T.size();
			if(prev == 1) len[T.first()] += Q.peek()[0]-pos;
			if(prev > 0) tot += Q.peek()[0]-pos;
			int now = Q.peek()[0];
			while(!Q.isEmpty() && Q.peek()[0] == now) {
				int info = Q.peek()[1];
				if(info == 1) T.add(Q.poll()[2]);
				else T.remove(Q.poll()[2]);
			}
			pos = now;
		}
		
		int ans = 0;
		for(int i=0;i<N;i++) ans = Math.max(ans, tot-len[i]);
		bw.write(ans + "\n");
		
		
		
	}
	
}

```
