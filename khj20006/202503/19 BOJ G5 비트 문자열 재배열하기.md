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
	
	static int N, M;
	static int start = 0, end1 = 0, end2 = 0;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = nextInt();
		M = nextInt();
		for(int i=N-1;i>=0;i--) if(nextInt() == 1) start |= (1<<i);
		int[] temp = new int[M];
		for(int i=0;i<M;i++) temp[i] = nextInt();
		int x = 0, y = 0;
		for(int i=M-1;i>=0;i--) {
			if(i%2 == 0) {
				x += temp[i];
				for(int j=0;j<temp[i];j++) end1 |= (1<<y++);
			}
			else {
				y += temp[i];
				for(int j=0;j<temp[i];j++) end2 |= (1<<x++);
			}
		}
		
	}
	
	static void solve() throws Exception{

		boolean[] vis = new boolean[32768];
		vis[start] = true;
		Queue<int[]> Q = new LinkedList<>();
		Q.offer(new int[] {start,0});
		while(!Q.isEmpty()) {
			int[] now = Q.poll();
			int n = now[0], t = now[1];
			if(n == end1 || n == end2) {
				bw.write(t+"\n");
				return;
			}
			for(int i=0;i<N-1;i++) {
				int x = (1<<i) * ((n&(1<<i)) == 0 ? 0 : 1);
				int y = (1<<(i+1)) * ((n&(1<<(i+1))) == 0 ? 0 : 1);
				int next = n^x^y;
				next |= (x<<1) | (y>>1);
				if(!vis[next]) {
					vis[next] = true;
					Q.offer(new int[] {next,t+1});
				}
			}
		}

	}
	
}

```
