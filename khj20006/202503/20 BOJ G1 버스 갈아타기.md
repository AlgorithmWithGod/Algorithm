```java

import java.util.*;
import java.io.*;

class Bus{
	int x1, y1, x2, y2;
	Bus(int x1, int y1, int x2, int y2){
		this.x1 = x1;
		this.y1 = y1;
		this.x2 = x2;
		this.y2 = y2;
	}
	
	boolean intersect(Bus other) {
		
		if(this.x1 == this.x2 && other.x1 == other.x2) {
			if(this.x1 != other.x1) return false; 
			if(this.y1 > other.y2 || this.y2 < other.y1) return false;
			return true;
		}
		
		if(this.y1 == this.y2 && other.y1 == other.y2) {
			if(this.y1 != other.y1) return false;
			if(this.x1 > other.x2 || this.x2 < other.x1) return false;
			return true;
		}
		
		if(this.x1 == this.x2) {
			if(other.x1 <= this.x1 && this.x1 <= other.x2 && this.y1 <= other.y1 && other.y1 <= this.y2) {
				return true;
			}
			
			return false;
		}
		if(other.y1 <= this.y1 && this.y1 <= other.y2 && this.x1 <= other.x1 && other.x1 <= this.x2) {
			return true;
		}
		
		return false;
	}
}

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
	
	static int M, N, K, sx, sy, ex, ey;
	static Bus[] bs;
	static boolean[] starts, ends;
	
	static boolean[][] V;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		M = nextInt();
		N = nextInt();
		K = nextInt();
		bs = new Bus[K];
		V = new boolean[K][K];
		for(int i=0;i<K;i++) {
			int id = nextInt(), x1 = nextInt(), y1 = nextInt(), x2 = nextInt(), y2 = nextInt();
			if(x1 == x2) {
				int min = Math.min(y1, y2);
				int max = Math.max(y1, y2);
				y1 = min;
				y2 = max;
			}
			else {
				int min = Math.min(x1, x2);
				int max = Math.max(x1, x2);
				x1 = min;
				x2 = max;
			}
			bs[i] = new Bus(x1,y1,x2,y2);
		}
		sx = nextInt();
		sy = nextInt();
		ex = nextInt();
		ey = nextInt();
		starts = new boolean[K];
		ends = new boolean[K];
		
	}
	
	static void solve() throws Exception{

		for(int i=0;i<K;i++) {
			for(int j=i+1;j<K;j++) {
				if(bs[i].intersect(bs[j])) {
					V[i][j] = true;
					V[j][i] = true;
				}
			}
		}
		
		for(int i=0;i<K;i++) {
			if(bs[i].intersect(new Bus(sx,sy,sx,sy))) starts[i] = true;
			if(bs[i].intersect(new Bus(ex,ey,ex,ey))) ends[i] = true;
		}
		
		Queue<int[]> Q = new LinkedList<>();
		boolean[] vis = new boolean[K];
		for(int i=0;i<K;i++) if(starts[i]) {
			vis[i] = true;
			Q.offer(new int[] {i,1});
		}
		while(!Q.isEmpty()) {
			int[] now = Q.poll();
			int n = now[0], t = now[1];
			if(ends[n]) {
				bw.write(t + "\n");
				return;
			}
			for(int i=0;i<K;i++) if(i!=n && V[n][i] && !vis[i]) {
				vis[i] = true;
				Q.offer(new int[] {i,t+1});
			}
		}
	}
	
}

```
