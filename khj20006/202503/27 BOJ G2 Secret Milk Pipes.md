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
	
	static int W, P;
	static int[][] Edges;
	
	static List<int[]>[] V;
	static int[] r;
	
	static int f(int x) {return x==r[x] ? x : (r[x]=f(r[x]));}
	
	public static void main(String[] args) throws Exception {
			
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		W = nextInt();
		P = nextInt();
		Edges = new int[P][3];
		for(int i=0;i<P;i++) for(int j=0;j<3;j++) Edges[i][j] = nextInt();
		
		V = new List[W+1];
		r = new int[W+1];
		for(int i=1;i<=W;i++) {
			V[i] = new ArrayList<>();
			r[i] = i;
		}
		
	}
	
	static void solve() throws Exception{

		
		Arrays.sort(Edges, (a,b) -> a[2]-b[2]);
		
		int mst = 0;
		boolean[] used = new boolean[P];
		for(int i=0;i<P;i++) {
			int[] e = Edges[i];
			int a = e[0], b = e[1], c = e[2];
			int x = f(a), y = f(b);
			if(x == y) continue;
			mst += c;
			V[a].add(new int[] {b,c});
			V[b].add(new int[] {a,c});
			r[x] = y;
			used[i] = true;
		}
		
		int min = (int)1e9;
		for(int i=0;i<P;i++) if(!used[i]) {
			int[] e = Edges[i];
			int a = e[0], b = e[1], c = e[2];
			
			Queue<int[]> Q = new LinkedList<>();
			boolean[] vis = new boolean[W+1];
			
			Q.offer(new int[] {a,0});
			vis[a] = true;
			while(!Q.isEmpty()) {
				int[] now = Q.poll();
				int n = now[0], t = now[1];
				if(n == b) {
					min = Math.min(min, c-t);
					break;
				}
				for(int[] j:V[n]) if(!vis[j[0]]) {
					vis[j[0]] = true;
					Q.offer(new int[] {j[0],Math.max(t, j[1])});
				}
			}
			
		}
		bw.write((mst+min)+"\n");
	}
	
}

```
