```java
import java.util.*;
import java.io.*;

public class Main {
	
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
	
	static int N, M;
	static long[] b, c, l, s;
	static long ans = 0;
	static PriorityQueue<Long>[] Q;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
		
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = nextInt();
		M = nextInt();
		b = new long[N+1];
		c = new long[N+1];
		l = new long[N+1];
		s = new long[N+1];
		Q = new PriorityQueue[N+1];
		for(int i=1;i<=N;i++) {
			b[i] = nextInt();
			c[i] = nextInt();
			l[i] = nextInt();
			s[i] = c[i];
			Q[i] = new PriorityQueue<>((a,b) -> Long.compare(b, a));
			Q[i].add(c[i]);
			ans = Math.max(ans, l[i]);
		}
		
		
	}
	
	static void solve() throws Exception {
		
		for(int i=N;i>1;i--) {
			int p = (int)b[i];
			if(Q[i].size() > Q[p].size()) {
				Q[i].addAll(Q[p]);
				s[i] += s[p];
				Q[p] = Q[i];
				s[p] = s[i];
			}
			else {
				Q[p].addAll(Q[i]);
				s[p] += s[i];
			}
			while(s[p] > M) s[p] -= Q[p].poll();
			ans = Math.max(ans, l[p] * Q[p].size());
		}
		
		bw.write(ans + "\n");
		
	}
	
}
```
