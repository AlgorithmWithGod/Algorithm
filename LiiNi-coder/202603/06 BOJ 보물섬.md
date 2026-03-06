```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main{
	private static int N;
	private static int M;
	private static char[][] Map;
	private static final int[][] Drdcs = {
		{1,0},{-1,0},{0,1},{0,-1}
	};

	public static void main(String[] args)throws IOException{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		String[] temp = br.readLine().split(" ");
		N = Integer.parseInt(temp[0]);
		M = Integer.parseInt(temp[1]);

		Map = new char[N][M];
		for(int i=0; i<N; i++){
			Map[i] = br.readLine().toCharArray();
		}
		int answer = 0;
		for(int r=0; r<N; r++){
			for(int c=0; c<M; c++){
				if(Map[r][c]=='L'){
					answer = Math.max(answer, bfs(r,c));
				}
			}
		}
		System.out.println(answer);
	}

	private static int bfs(int sr,int sc){
		boolean[][] visited = new boolean[N][M];
		Deque<int[]> q = new ArrayDeque<int[]>();

		q.offer(new int[]{sr, sc, 0});
		visited[sr][sc] = true;

		int maxDist = 0;

		while(!q.isEmpty()){
			int[] qItem = q.poll();
			int r = qItem[0];
			int c = qItem[1];
			int dist = qItem[2];
			maxDist = Math.max(maxDist, dist);

			for(int i=0; i<4; i++){
				int nr = r + Drdcs[i][0];
				int nc = c + Drdcs[i][1];
				if(nr<0 || nc<0|| nr>=N || nc>=M)continue;
				if(visited[nr][nc])continue;
				if(Map[nr][nc]=='W')continue;

				visited[nr][nc] = true;
				q.offer(new int[]{nr, nc, dist+1});
			}
		}

		return maxDist;
	}
}
```
