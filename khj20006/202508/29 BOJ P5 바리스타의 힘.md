```java
import java.util.*;
import java.io.*;

class IOController {
	BufferedReader br;
	BufferedWriter bw;
	StringTokenizer st;

	public IOController() {
		br = new BufferedReader(new InputStreamReader(System.in));
		bw = new BufferedWriter(new OutputStreamWriter(System.out));
		st = new StringTokenizer("");
	}

	String nextLine() throws Exception {
		String line = br.readLine();
		st = new StringTokenizer(line);
		return line;
	}

	String nextToken() throws Exception {
		while (!st.hasMoreTokens()) nextLine();
		return st.nextToken();
	}

	int nextInt() throws Exception {
		return Integer.parseInt(nextToken());
	}

	long nextLong() throws Exception {
		return Long.parseLong(nextToken());
	}

	double nextDouble() throws Exception {
		return Double.parseDouble(nextToken());
	}

	void close() throws Exception {
		bw.flush();
		bw.close();
	}

	void write(String content) throws Exception {
		bw.write(content);
	}

}

public class Main {

	static IOController io;

	//

	static final int INF = (int)1e9 + 7;
	static final int[] dx = {1,0,-1,0};
	static final int[] dy = {0,1,0,-1};

	static int N, M;
	static boolean[][] wall;

	public static void main(String[] args) throws Exception {

		io = new IOController();

		N = io.nextInt();
		M = io.nextInt();
		wall = new boolean[N][M];
		for(int i=0;i<N;i++) {
			char[] tmp = io.nextToken().toCharArray();
			for(int j=0;j<M;j++) wall[i][j] = tmp[j] == '1';
		}

		int[][] from = bfs(0,0, false);
		int[][] to = bfs(N-1,M-1, true);

		int[][] right = new int[N][M];
		for(int i=0;i<N;i++) {
			right[i][M-1] = Math.min(INF, to[i][M-1] + M-1);
			for(int j=M-2;j>=0;j--) {
				right[i][j] = Math.min(right[i][j+1], to[i][j] + j);
			}
		}

		int[][] up = new int[N][M];
		for(int j=0;j<M;j++) {
			up[N-1][j] = Math.min(INF, to[N-1][j] + N-1);
			for(int i=N-2;i>=0;i--) {
				up[i][j] = Math.min(up[i+1][j], to[i][j] + i);
			}
		}

		int ans = INF;
		for(int i=0;i<N;i++) for(int j=0;j<M;j++) if(from[i][j] != INF) {
			int res = Math.min(from[i][j] + right[i][j] - j, from[i][j] + up[i][j] - i);
			ans = Math.min(ans, res);
		}
		io.write((ans == INF ? "-1" : ans) + "\n");

		io.close();

	}

	static int[][] bfs(int a, int b, boolean can) {
		int[][] res = new int[N][M];
		for(int i=0;i<N;i++) Arrays.fill(res[i], INF);

		boolean[][] vis = new boolean[N][M];
		Queue<int[]> q = new ArrayDeque<>();
		q.offer(new int[]{a,b,0});
		vis[a][b] = true;
		while(!q.isEmpty()) {
			int[] cur = q.poll();
			int x = cur[0], y = cur[1], t = cur[2];
			res[x][y] = t;
			for(int i=0;i<4;i++) {
				int xx = x+dx[i], yy = y+dy[i];
				if(xx<0 || xx>=N || yy<0 || yy>=M || vis[xx][yy]) continue;
				if(wall[xx][yy]) {
					if(can) {
						res[xx][yy] = t+1;
						vis[xx][yy] = true;
					}
					continue;
				}
				q.offer(new int[]{xx,yy,t+1});
				vis[xx][yy] = true;
			}
		}
		return res;
	}

}
```
