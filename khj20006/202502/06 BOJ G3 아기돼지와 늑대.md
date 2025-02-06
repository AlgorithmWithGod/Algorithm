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
	static char[][] arr;
	static boolean[][] vis;
	static int[] dx = {1,0,-1,0};
	static int[] dy = {0,1,0,-1};
	
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
		vis = new boolean[N][M];
		for(int i=0;i<N;i++) arr[i] = br.readLine().toCharArray();
		
	}
	
	static void solve() throws Exception{

		Queue<int[]> Q = new LinkedList<>();
		for(int i=0;i<N;i++) for(int j=0;j<M;j++) if(arr[i][j] == 'W') {
			Q.add(new int[] {i,j});
			vis[i][j] = true;
		}
		
		while(!Q.isEmpty()) {
			int[] temp = Q.poll();
			int x = temp[0], y = temp[1];
			
			for(int i=0;i<4;i++) {
				int xx = x+dx[i], yy = y+dy[i];
				while(arr[xx][yy] == '+') {
					xx += dx[i];
					yy += dy[i];
				}
				
				if(arr[xx][yy] == '#') {
					xx -= dx[i];
					yy -= dy[i];
				}
				
				if(vis[xx][yy]) continue;
				Q.offer(new int[] {xx,yy});
				vis[xx][yy] = true;
				
			}
			
		}
		
		for(int i=0;i<N;i++) {
			for(int j=0;j<M;j++) {
				if(arr[i][j] == '.' && !vis[i][j]) bw.write('P');
				else bw.write(arr[i][j]);
			}
			bw.write("\n");
		}
		
		
	}
	
}

```
