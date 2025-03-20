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
	
	static int R, C;
	static int pr, pc, kr, kc;
	
	static int[] dx = {-2,-2,-1,-1,1,1,2,2};
	static int[] dy = {-1,1,-2,2,-2,2,-1,1};
	
	public static void main(String[] args) throws Exception {
		
		for(int T=nextInt();T-->0;) {
			
			ready();
			solve();
		}
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		R = nextInt();
		C = nextInt();
		pr = nextInt();
		pc = nextInt();
		kr = nextInt();
		kc = nextInt();
		
	}
	
	static void solve() throws Exception{

		int[][] time = new int[R+1][C+1];
		for(int i=1;i<=R;i++) Arrays.fill(time[i], -1);
		
		time[kr][kc] = 0;
		Queue<int[]> Q = new LinkedList<>();
		
		int win = -1;
		int stalemate = -1;
		Q.offer(new int[] {kr,kc,0});
		while(!Q.isEmpty()) {
			int[] now = Q.poll();
			int x = now[0], y = now[1], t = now[2];
			if(y == pc) {
				if(x<R && pr+t <= x && (x-pr-t)%2 == 0) {
					if(win == -1) win = x-pr;
					else win = Math.min(win, x-pr);
				}
				if(pr+t+1 <= x && (x-pr-t-1)%2 == 0) {
					if(stalemate == -1) stalemate = x-pr-1;
					else stalemate = Math.min(stalemate, x-pr-1);
				}
				
			}
			for(int i=0;i<8;i++) {
				int xx = x+dx[i], yy = y+dy[i];
				if(xx<1 || xx>R || yy<1 || yy>C || time[xx][yy]!=-1) continue;
				time[xx][yy] = t+1;
				Q.offer(new int[] {xx,yy,t+1});
			}
		}
		if(win != -1) bw.write("Win in " + Math.max(win, 0) + " knight move(s).\n");
		else if(stalemate != -1) bw.write("Stalemate in " + stalemate + " knight move(s).\n");
		else bw.write("Loss in " + Math.max(R-pr-1, 0) + " knight move(s).\n");
		
	}
	
}

```
