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

	static int N;
	static int[][] A;
	
	static int[] dx = {1,0,-1,0};
	static int[] dy = {0,1,0,-1};
	
	public static void main(String[] args) throws Exception {
			
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = Integer.parseInt(br.readLine());
		A = new int[N][N];
		for(int i=0;i<N;i++) {
			nextLine();
			for(int j=0;j<N;j++) A[i][j] = nextInt();
		}
		
	}
	
	static void solve() throws Exception{
		
		int ans = Integer.MAX_VALUE;
		while(A[0][0] >= 0) {
			ans = Math.min(ans, findMin());
			reduce();
		}
		bw.write(ans + "\n");
		
	}
	
	static void reduce() {
		for(int i=0;i<N;i++) for(int j=0;j<N;j++) A[i][j]--;
	}
	
	static int findMin() {
		
		int s = 0, e = 200, m = (s+e)>>1;
		// m이하인 칸들로만 도달할 수 있는지?
		while(s<e) {
			if(bfs(m)) e = m;
			else s = m+1;
			m = (s+e)>>1;
		}
		return m;
		
	}
	
	// limit 제한 내에서의 bfs
	static boolean bfs(int limit) {
		
		if(A[0][0] > limit) return false;
		
		Queue<int[]> Q = new LinkedList<>();
		boolean[][] vis = new boolean[N][N];
		Q.offer(new int[] {0,0});
		vis[0][0] = true;
		while(!Q.isEmpty()) {
			
			int[] now = Q.poll();
			int x = now[0], y = now[1];
			if(x == N-1 && y == N-1) return true;
			for(int i=0;i<4;i++) {
				int xx = x+dx[i], yy = y+dy[i];
				if(safe(xx,yy) && A[xx][yy] <= limit && A[xx][yy] >= 0 && !vis[xx][yy]) {
					vis[xx][yy] = true;
					Q.offer(new int[] {xx,yy});
				}
			}
			
		}
		
		return false;
		
	}
	
	static boolean safe(int x, int y) {
		return 0<=x&&x<N && 0<=y&&y<N;
	}
	
}

```
