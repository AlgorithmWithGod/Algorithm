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
	
	static int N, M;
	static char[][] A;
	static int[] start;
	
	static int[] dx = {1,0,-1,0};
	static int[] dy = {0,1,0,-1};
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = nextInt();
		M = nextInt();
		A = new char[N][M];
		for(int i=0;i<N;i++) {
			A[i] = br.readLine().toCharArray();
			for(int j=0;j<M;j++) if(A[i][j] == '0') start = new int[] {i,j};
		}
		
	}
	
	static void solve() throws Exception{
		
		boolean[][][] vis = new boolean[N][M][64];
		Queue<int[]> Q = new LinkedList<>();
		vis[start[0]][start[1]][0] = true;
		Q.offer(new int[] {start[0], start[1], 0, 0});
		while(!Q.isEmpty()) {
			int[] now = Q.poll();
			int x = now[0], y = now[1], keys = now[2], t = now[3];
			if(A[x][y] == '1') {
				bw.write(t + "\n");
				return;
			}
			for(int i=0;i<4;i++) {
				int xx = x+dx[i], yy = y+dy[i];
				if(xx<0 || xx>=N || yy<0 || yy>=M || A[xx][yy] == '#') continue;
				int nkeys = keys;
				if(A[xx][yy] >= 'a') nkeys |= (1<<(A[xx][yy]-'a'));
				if('A' <= A[xx][yy] && A[xx][yy] <= 'F' && (nkeys & (1<<(A[xx][yy]-'A'))) == 0) continue; 
				if(vis[xx][yy][nkeys]) continue;
				vis[xx][yy][nkeys] = true;
				Q.offer(new int[] {xx,yy,nkeys,t+1});
			}
		}
		bw.write("-1");
		
	}
	
}

```
