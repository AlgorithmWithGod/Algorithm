```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayDeque;
import java.util.Arrays;

public class B1261 {

	private static BufferedReader br;
	private static int m;
	private static int n;
	private static int[][] map;
	private static ArrayDeque<int[]> q;
	private static int[][] drdcs = new int[][] {
		{0, 1},
		{1, 0},
		{-1, 0},
		{0, -1}
	};
	private static int[][] visited;
	public static void main(String[] args) throws IOException {
		br = new BufferedReader(new InputStreamReader(System.in));
		String[] temp = br.readLine().split(" ");
		m = Integer.parseInt(temp[0]);
		n = Integer.parseInt(temp[1]);
		map = new int[n][m];
		//[i][j]에서 벽을 부순 것의 최소를 담는 배열
		visited = new int[n][m];
		for(int r = 0; r<n; r++) {
			String line = br.readLine();
			for(int c = 0; c<m; c++) {
				if(line.charAt(c) == '1') {
					map[r][c] = 1;
				}else
					map[r][c] = 0;
				visited[r][c] = Integer.MAX_VALUE;
			}
		}
		
		q = new ArrayDeque<int[]>();
		q.add(new int[] {0, 0, 0});
		
		int[] goal = new int[] {n-1, m-1};
		int answer = 100*100;
		while(!q.isEmpty()) {
			int[] temp1 = q.poll();
			int[] p = Arrays.copyOfRange(temp1, 0, 2);
			int countOfBreakingWall = temp1[2];
			// 종료조건
			if(isSamePoint(p, goal)) {
				if(countOfBreakingWall==0) {
					answer = 0;
					break;
				}
				else {
					answer = Math.min(answer, countOfBreakingWall);
					continue;
				}
			}
			for(int[] drdc : drdcs ) {
				int[] nextPoint = new int[]{p[0] + drdc[0], p[1]+ drdc[1]};
				if(nextPoint[0] < 0 || nextPoint[0] >= n || nextPoint[1] < 0 || nextPoint[1] >= m)
					continue;
				int nextCountOfBreakingWall = countOfBreakingWall;
				//벽이면
				if(getValueAtPoint(map, nextPoint) == 1) {
					if(getValueAtPoint(visited, nextPoint) > nextCountOfBreakingWall) {
						nextCountOfBreakingWall++;
						visited[p[0]][p[1]] = countOfBreakingWall;
						q.addLast(new int[] {nextPoint[0], nextPoint[1], nextCountOfBreakingWall});
					}
				}else {
					if(getValueAtPoint(visited, nextPoint) > nextCountOfBreakingWall) {
						visited[p[0]][p[1]] = countOfBreakingWall;
						q.addFirst(new int[] {nextPoint[0], nextPoint[1], nextCountOfBreakingWall});
					}
				}
			}
		}
		
		System.out.println(answer);
	}

	private static int getValueAtPoint(int[][] matrix, int[] p) {
		return matrix[p[0]][p[1]];
	}

	private static boolean isSamePoint(int[] p, int[] q) {
		return p[0] == q[0] && p[1] == q[1];
	}

}
```
