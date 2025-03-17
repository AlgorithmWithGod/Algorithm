```java

import java.util.*;
import java.io.*;

public class Main {

	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
	static StringTokenizer st = new StringTokenizer("");
	
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() throws Exception {
		if(!st.hasMoreTokens()) nextLine();
		return Integer.parseInt(st.nextToken());
	}
	static long nextLong() throws Exception {
		if(!st.hasMoreTokens()) nextLine();
		return Long.parseLong(st.nextToken());
	}
	static void ioClose() throws Exception {bw.flush();bw.close();br.close();}
	
	/*
	 * [solving strategy]
	 * 기차의 왼쪽 위의 점 (x,y)를 잡고, 기차의 방향(dir)을 추가하면
	 * 각 상태 (x,y,dir)의 관점에서 보면 항상 최단 거리로 각 상태에 도달하는 것이 이득입니다.
	 * 따라서, 적절히 시작점을 찾아 3차원 필드에서 BFS를 수행합니다.
	 * 
	 * [description]
	 * - N : 공간의 한 변의 길이
	 * - A : 공간의 정보
	 * - dx, dy : 4방향 탐색을 위한 x, y의 변홧값 배열
	 * 
	 * - ready() : input 처리
	 * - solve() : 초기 상태 확인, bfs 호출하여 정답 도출
	 * - bfs(sx,sy,sdir) : 초기 상태를 (sx,sy,sdir)로 두고 3차원 필드에서 BFS 수행
	 * - canRotate(x,y,dir) : 주어진 상태 (x,y,dir)에서 올바르게 회전시킬 수 있는지 확인, boolean 형으로 반환
	 * - isEnd(x,y,dir) : 현재 상태 (x,y,dir)이 목적지의 상태와 동일한지 확인, boolean 형으로 반환
	 * - safe(x,y,dir) : 상태 (x,y,dir)이 유효한 상태인지 확인, boolean 형으로 반환 
	 */
	
	static int N;
	static char[][] A;
	static int[] dx = {1,0,-1,0};
	static int[] dy = {0,1,0,-1};
	
	public static void main(String[] args) throws Exception {
		//--------------솔루션 코드를 작성하세요.--------------------------------
		
		ready();
		solve();
		
		ioClose();
		
	}
	
	static void ready() throws Exception {
		
		N = nextInt();
		A = new char[N][];
		for(int i=0;i<N;i++) A[i] = br.readLine().toCharArray();
		
	}
	
	static void solve() throws Exception {
		
		for(int i=0;i<N;i++) for(int j=0;j<N;j++) if(A[i][j] == 'B') {
			int dir = 1;
			if(i<N-1 && A[i+1][j] == 'B') dir = 0;
			bw.write(bfs(i,j,dir) + "\n");
			return;
		}
		
	}
	
	static int bfs(int sx, int sy, int sdir) {
		
		Queue<int[]> Q = new LinkedList<>();
		boolean[][][] vis = new boolean[N][N][2];
		
		vis[sx][sy][sdir] = true;
		Q.offer(new int[] {sx,sy,sdir,0});
		
		while(!Q.isEmpty()) {
			int[] now = Q.poll();
			int x = now[0], y = now[1], dir = now[2], t = now[3];
			if(isEnd(x,y,dir)) return t;
			
			if(canRotate(x,y,dir)) {
				if(dir == 0) {
					if(!vis[x+1][y-1][1]) {
						vis[x+1][y-1][1] = true;
						Q.offer(new int[] {x+1,y-1,1,t+1});
					}					
				}
				else {
					if(!vis[x-1][y+1][0]) {
						vis[x-1][y+1][0] = true;
						Q.offer(new int[] {x-1,y+1,0,t+1});
					}
				}
			}
			
			for(int i=0;i<4;i++) {
				int xx = x+dx[i], yy = y+dy[i];
				if(safe(xx,yy,dir) && !vis[xx][yy][dir]) {
					vis[xx][yy][dir] = true;
					Q.offer(new int[] {xx,yy,dir,t+1});
				}
			}
			
		}
		
		return 0;
		
	}
	
	static boolean canRotate(int x, int y, int dir) {
		if(dir == 0) {
			if(0<=y-1 && y+1<N) {
				for(int xx=x;xx<=x+2;xx++) for(int yy=y-1;yy<=y+1;yy++) {
					if(A[xx][yy] == '1') return false;
				}
			}
			else return false;
		}
		else {
			if(0<=x-1 && x+1<N) {
				for(int xx=x-1;xx<=x+1;xx++) for(int yy=y;yy<=y+2;yy++) {
					if(A[xx][yy] == '1') return false;
				}
			}
			else return false;
		}
		return true;
	}
	
	static boolean isEnd(int x, int y, int dir) {
		if(A[x][y] != 'E') return false;
		if(dir == 0) return A[x+1][y] == 'E' && A[x+2][y] == 'E';
		return A[x][y+1] == 'E' && A[x][y+2] == 'E';
	}
	
	static boolean safe(int x, int y, int dir) {
		boolean res = 0<=x && x<N && 0<=y && y<N && A[x][y] != '1';
		if(!res) return res;
		if(dir == 0)	res &= x+2 < N && A[x+1][y] != '1' && A[x+2][y] != '1';
		else	 		res &= y+2 < N && A[x][y+1] != '1' && A[x][y+2] != '1';
		return res;
	}

}

```
