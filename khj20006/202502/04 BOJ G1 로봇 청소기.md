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
	static int INF = (int)1e8 + 1;
	
	static int H, W;
	static int[][] dist;
	static char[][] arr;
	static int[] X;
	static int[] Y;
	static int ans;
	
	static void initialize() {
		dist = new int[11][11];
		arr = new char[H][W];
		X = new int[11];
		Y = new int[11];
		for(int i=0;i<=10;i++) Arrays.fill(dist[i], INF);
		ans = INF;
	}
	
	static boolean inside(int x, int y) {
		return 0<=x&&x<H && 0<=y&&y<W;
	}
	
	static void bfs(int s) {
		boolean[][] vis = new boolean[H][W];
		vis[X[s]][Y[s]] = true;
		Queue<int[]> Q = new LinkedList<>();
		Q.offer(new int[] {X[s],Y[s],0});
		while(!Q.isEmpty()) {
			int[] now = Q.poll();
			int x = now[0], y = now[1], t = now[2];
			if('A' <= arr[x][y] && arr[x][y] <= 'Z') {
				dist[s][arr[x][y]-'A'] = t;
			}
			for(int i=0;i<4;i++) {
				int xx = x+dx[i], yy = y+dy[i];
				if(inside(xx,yy) && !vis[xx][yy] && arr[xx][yy] != 'x') {
					Q.offer(new int[] {xx,yy,t+1});
					vis[xx][yy] = true;
				}
			}
		}
	}
	
	static void exSearch(int cnt, int choose, int now, int prev, int time, int limit) {
		if(cnt == limit) {
			ans = Math.min(ans, time);
			return;
		}
		for(int i=1;i<=limit;i++) {
			if((choose & (1<<i)) == 0) exSearch(cnt+1,choose | (1<<i), i, now, time + dist[now][i], limit);
		}
	}
	
	static void solve() throws Exception{
		
		initialize();
		
		int num = 1;
		char temp = 'B';
		for(int i=0;i<H;i++) {
			String line = br.readLine();
			for(int j=0;j<W;j++) {
				arr[i][j] = line.charAt(j);
				if(arr[i][j] == '*') {
					arr[i][j] = temp++; 
					X[num] = i;
					Y[num] = j;
					num++;
				}
				else if(arr[i][j] == 'o') {
					arr[i][j] = 'A';
					X[0] = i;
					Y[0] = j;
				}
			}
		}
		
		for(int i=0;i<num;i++) bfs(i);
		
		for(int i=1;i<num;i++) exSearch(1,(1<<i),i,0,dist[0][i],num-1);
		
		if(ans >= INF) bw.write("-1\n");
		else bw.write(ans+"\n");
		
	}
	
	public static void main(String[] args) throws Exception {

		nextLine();
		W = nextInt();
		H = nextInt();
		while(H != 0) {
			solve();
			nextLine();
			W = nextInt();
			H = nextInt();
		}
		
		
		bwEnd();
	}

}

```
