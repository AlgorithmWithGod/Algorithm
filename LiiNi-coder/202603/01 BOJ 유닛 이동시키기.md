```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayDeque;
import java.util.Deque;
import java.util.StringTokenizer;

public class Main {
	private static int N;
	private static int M;
	private static int A;
	private static int B;
	private static int[][] board;
	private static boolean[][] visited;
	private static final int[][] Drdcs = {
		{1, 0},
		{0, 1},
		{-1, 0},
		{0, -1}
	};
	public static void main(String[] args)throws IOException{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		N = Integer.parseInt(st.nextToken());
		M = Integer.parseInt(st.nextToken());
		A = Integer.parseInt(st.nextToken());
		B = Integer.parseInt(st.nextToken());
		int K = Integer.parseInt(st.nextToken());
		board = new int[N+1][M+1];
		visited = new boolean[N+1][M+1];
		for(int i=0; i<K;i++){
			st = new StringTokenizer(br.readLine());
			int r = Integer.parseInt(st.nextToken());
			int c = Integer.parseInt(st.nextToken());
			board[r][c] = 1;
		}
		st = new StringTokenizer(br.readLine());
		int sr = Integer.parseInt(st.nextToken());
		int sc = Integer.parseInt(st.nextToken());
		st = new StringTokenizer(br.readLine());
		int er = Integer.parseInt(st.nextToken());
		int ec = Integer.parseInt(st.nextToken());

		System.out.println(bfs(sr,sc,er,ec));
	}

	private static int bfs(int sr, int sc, int er, int ec){
		Deque<int[]> q = new ArrayDeque<>();
		q.offer(new int[]{sr, sc, 0});
		visited[sr][sc] = true;
		while(!q.isEmpty()){
			int[] cur = q.poll();
			int r = cur[0];
			int c = cur[1];
			int dist = cur[2];
			if(r==er && c==ec){
				return dist;
			}

			for(int i=0;i<4;i++){
				int nr = r + Drdcs[i][0];
				int nc = c + Drdcs[i][1];

				if(nr<1||nc<1||nr+A-1>N||nc+B-1>M) continue;
				if(visited[nr][nc]) continue;
				if(isBlocked(nr,nc)) continue;
				visited[nr][nc] = true;
				q.offer(new int[]{nr,nc,dist+1});
			}
		}

		return -1;
	}

	private static boolean isBlocked(int r, int c){
		for(int i=r; i<r+A; i++){
			for(int j=c; j<c+B; j++){
				if(board[i][j]==1){
					return true;
				}
			}
		}
		return false;
	}
}
```
