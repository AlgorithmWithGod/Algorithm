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
	
	static int N, M, K;
	static List<int[]>[] V;
	
	static final long INF = (long)1e18 + 7;
	
	public static void main(String[] args) throws Exception {
			
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = nextInt();
		M = nextInt();
		K = nextInt();
		V = new List[N+1];
		for(int i=1;i<=N;i++) V[i] = new ArrayList<>();
		for(int i=0;i<M;i++) {
			int a = nextInt(), b = nextInt(), c = nextInt();
			V[b].add(new int[] {a,c});
		}
		
	}
	
	static void solve() throws Exception{
		
		PriorityQueue<long[]> Q = new PriorityQueue<>((a,b) -> {
			if(a[0] < b[0]) return -1;
			if(a[0] > b[0]) return 1;
			return 0;
		});
		long[] D = new long[N+1];
		Arrays.fill(D, INF);
		for(int i=0;i<K;i++) {
			int k = nextInt();
			D[k] = 0;
			Q.offer(new long[] {0,k});
		}
		
		while(!Q.isEmpty()) {
			long[] now = Q.poll();
			long d = now[0];
			int n = (int)now[1];
			if(d > D[n]) continue;
			for(int[] next:V[n]) {
				int i = next[0], c = next[1];
				if(D[i] > d+c) {
					D[i] = d+c;
					Q.offer(new long[] {D[i],i});
				}
			}
		}
		
		long num = -1, dist = -1;
		for(int i=1;i<=N;i++) if(D[i] != INF) {
			if(D[i] > dist) {
				num = i;
				dist = D[i];
			}
		}
		bw.write(num + "\n" + dist);
		
	}
	
}

```
