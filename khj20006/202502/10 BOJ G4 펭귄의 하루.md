```java

import java.util.*;
import java.io.*;


class Main {
	
	// IO field
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
	static StringTokenizer st;

	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	static long nextLong() {return Long.parseLong(st.nextToken());}
	static void bwEnd() throws Exception {bw.flush();bw.close();}
	
	// Additional field
	static int[] dx = {1,0,-1,0};
	static int[] dy = {0,1,0,-1};
	
	static char[][] arr;
	static boolean[][][] vis;
	static int N, M;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
	}
	
	static void ready() throws Exception{
		nextLine();
		N = nextInt();
		M = nextInt();
		arr = new char[N][M];
		vis = new boolean[N][M][2];
		for(int i=0;i<N;i++) arr[i] = br.readLine().toCharArray();
		
	}
	
	static void solve() throws Exception{

		for(int i=0;i<N;i++) for(int j=0;j<M;j++) if(arr[i][j] == 'S') {
			bw.write(bfs(i,j)+"\n");
			return;
		}
		
	}
	
	static int bfs(int sx, int sy) throws Exception {
		
		Queue<int[]> Q = new LinkedList<>();
		vis[sx][sy][0] = true;
		Q.offer(new int[] {sx,sy,0,0});
		
		while(!Q.isEmpty()) {
			int[] now = Q.poll();
			int x = now[0], y = now[1], v = now[2], t = now[3];
			if(arr[x][y] == 'H' && v == 1) return t;
			
			for(int i=0;i<4;i++) {
				int xx = x+dx[i], yy = y+dy[i];
				if(xx<0 || xx>=N || yy<0 || yy>=M || arr[xx][yy] == 'D') continue;
				int vv = arr[xx][yy] == 'F' ? 1 : v;
				if(vis[xx][yy][vv]) continue;
				Q.offer(new int[] {xx,yy,vv,t+1});
				vis[xx][yy][vv] = true;
			}
		}
		return -1;
		
	}
	
}

```
