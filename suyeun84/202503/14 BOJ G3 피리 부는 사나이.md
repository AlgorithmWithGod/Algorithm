```java
import java.io.*;
import java.util.*;

public class boj16724 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    
	static boolean[][] visited, finished;
	static int answer;
	static int[][] board;
	static int[] dr = {-1,1,0,0};
	static int[] dc = {0,0,-1,1};
	public static void main(String[] args) throws Exception{
		StringTokenizer st = new StringTokenizer(br.readLine());

		int N = Integer.parseInt(st.nextToken());
		int M = Integer.parseInt(st.nextToken());
		
		board = new int[N][M];
		visited = new boolean[N][M];
		finished = new boolean[N][M];
		answer = 0;
		
		for(int i=0;i<N;i++) {
			String line = br.readLine();
			for(int j=0;j<M;j++) {
				int c = line.charAt(j);
				if(c == 'U') board[i][j] = 0;
				else if(c == 'D') board[i][j] = 1;
				else if(c == 'L') board[i][j] = 2;
				else if(c == 'R') board[i][j] = 3;
			}
		}
		
		for(int i=0;i<N;i++) {
			for(int j=0;j<M;j++) {
				if(!visited[i][j]) dfs(i,j);
			}
		}
		System.out.println(answer);
	}

	public static void dfs(int r, int c) {
		
		visited[r][c] = true;
		
		int nr = r + dr[board[r][c]];
		int nc = c + dc[board[r][c]];
		
		if(!visited[nr][nc]) {
			dfs(nr,nc);
		}else {
			if(!finished[nr][nc]) answer++;
		}
		finished[r][c] = true;
	}
}

```
