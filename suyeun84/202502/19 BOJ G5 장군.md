```java
import java.util.*;
import java.io.*;

public class Main {
	static Position king;
	public static void main(String[] args) throws Exception {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		
		int[][] dir = new int[][] {{-3,-2},{-3,2},{3,-2},{3,2},{2,-3},{-2,-3},{-2,3},{2,3}};
		Position sang;
		boolean[][] visited = new boolean[10][9];
		
		sang = new Position(Integer.parseInt(st.nextToken()), Integer.parseInt(st.nextToken()), 0);
		st = new StringTokenizer(br.readLine());
		king = new Position(Integer.parseInt(st.nextToken()), Integer.parseInt(st.nextToken()), 0);
		
		Queue<Position> q = new LinkedList<>();
		q.add(sang);
		visited[sang.y][sang.x] = true;
		while(!q.isEmpty()) {
			Position curr = q.poll();
			for (int[] d : dir) {
				int ny = curr.y + d[0];
				int nx = curr.x + d[1];
				if (ny >= 10 || ny < 0 || nx >= 9 || nx < 0 || visited[ny][nx]) continue;
				if (check(d, curr)) continue;
				if (ny == king.y && nx == king.x) {
					System.out.println(curr.m+1);
					return;
				}
				q.add(new Position(ny, nx, curr.m+1));
				visited[ny][nx] = true;
			}
		}
		System.out.println(-1);
	}
	static boolean check(int[] d, Position curr) {
		if (Math.abs(d[0]) == 2) {
			int ny = curr.y;
			int nx = curr.x + d[1]/3;
			if(ny == king.y && nx == king.x) return true;
			ny += d[0]/2;
			nx += d[1]/3;
			if(ny == king.y && nx == king.x) return true;
		} else {
			int ny = curr.y + d[0]/3;
			int nx = curr.x;
			if(ny == king.y && nx == king.x) return true;
			ny += d[0]/3;
			nx += d[1]/2;
			if(ny == king.y && nx == king.x) return true;
		}
		return false;
	}
	
	static class Position {
		int y;
		int x;
		int m;
		public Position(int y, int x, int m) {
			this.y = y;
			this.x = x;
			this.m = m;
		}
	}
}
```
