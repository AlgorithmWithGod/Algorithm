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
	
	static int N, M, S, E;
	static List<int[]>[] V;
	static boolean[] vis; 
	
	static final int INF = (int)1e9 + 5;
	
	public static void main(String[] args) throws Exception {
			
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = nextInt();
		M = nextInt();
		V = new List[N+1];
		for(int i=1;i<=N;i++) V[i] = new ArrayList<>();
		for(int i=0;i<M;i++) {
			int a = nextInt(), b = nextInt(), c = nextInt();
			V[a].add(new int[] {b,c});
			V[b].add(new int[] {a,c});
		}
		for(int i=1;i<=N;i++) Collections.sort(V[i], (a,b) -> a[0]-b[0]);
		S = nextInt();
		E = nextInt();
		vis = new boolean[N+1];
		
	}
	
	static void solve() throws Exception{
		
		int ans = 0;
		{
			PriorityQueue<int[]> Q = new PriorityQueue<>((a,b) -> {
				if(a[0] == b[0]) return a[1]-b[1];
				return a[0]-b[0];
			});
			int[] D = new int[N+1];
			Arrays.fill(D, INF);
			Q.offer(new int[] {0,E});
			D[E] = 0;
			while(!Q.isEmpty()) {
				int[] now = Q.poll();
				int d = now[0], n = now[1];
				if(d > D[n]) continue;
				for(int[] next:V[n]) {
					int i = next[0], c = next[1];
					if(D[i] > d+c) {
						D[i] = d+c;
						Q.offer(new int[] {D[i],i});
					}
				}
			}
			ans += D[S];
			int g = S;
			while(g != E) {
				for(int[] i:V[g]) if(D[g] == i[1] + D[i[0]]) {
					g = i[0];
					break;
				}
				if(g != E) vis[g] = true;
			}
			
		}
		
		
		PriorityQueue<int[]> Q = new PriorityQueue<>((a,b) -> {
			if(a[0] == b[0]) return a[1]-b[1];
			return a[0]-b[0];
		});
		int[] D = new int[N+1];
		Arrays.fill(D, INF);
		Q.offer(new int[] {0,E});
		D[E] = 0;
		while(!Q.isEmpty()) {
			int[] now = Q.poll();
			int d = now[0], n = now[1];
			if(d > D[n]) continue;
			for(int[] next:V[n]) if(!vis[next[0]]) {
				int i = next[0], c = next[1];
				if(D[i] > d+c) {
					D[i] = d+c;
					Q.offer(new int[] {D[i],i});
				}
			}
		}
		bw.write((ans + D[S]) + "\n");
		
	}
	
}

```
