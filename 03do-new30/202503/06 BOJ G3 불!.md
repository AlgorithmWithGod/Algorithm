```java
import java.util.*;
import java.io.*;
public class Main {
	
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static int R, C;
	static char[][] arr;
	static int[][] fireTime;
	static int[] dr = {0, 0, -1, 1};
	static int[] dc = {-1, 1, 0, 0};
	
	public static void main(String[] args) throws IOException{
		
		input();
		setFireTime();
		int result = bfs();
		System.out.println(result == -1 ? "IMPOSSIBLE" : result);
		
	}
	
	static int bfs() {
		int[][] time = new int[R][C];
		Queue<int[]> q = new ArrayDeque<>();
		for (int i = 0; i < R; i++) {
			for (int j = 0; j < C; j++) {
				if (arr[i][j] == 'J') {
					time[i][j] = 0;
					q.offer(new int[] {i, j});
				} else {
					time[i][j] = -1;
				}
			}
		}
		
		while (!q.isEmpty()) {
			int[] tmp = q.poll();
			int r = tmp[0];
			int c = tmp[1];
			for (int i = 0; i < 4; i++) {
				int nr = r + dr[i];
				int nc = c + dc[i];
				if (nr < 0 || nr >= R || nc < 0 || nc >= C) {
					// 탈출
					return time[r][c] + 1;
				}
				if (arr[nr][nc] != '.') { continue; }
				if (time[nr][nc] > -1) { continue; }
				// 불이 번진 시간보다 작아야 해당 칸으로 이동할 수 있다.
				if (fireTime[nr][nc] == -1 || fireTime[nr][nc] > time[r][c] + 1) {
					time[nr][nc] = time[r][c] + 1;
					q.offer(new int[] {nr, nc});
				}
			}
		}
		return -1;
	}
	
	static void setFireTime( ) { // 불이 번지는 시간을 기록한다.
		fireTime = new int[R][C];
		Queue<int[]> q = new ArrayDeque<>();
		for (int i = 0; i < R; i++) {
			for (int j = 0; j < C; j++) {
				if (arr[i][j] == 'F') {
					q.offer(new int[] {i, j});
					fireTime[i][j] = 0;
				} else {
					fireTime[i][j] = -1;
				}
			}
		}
		while (!q.isEmpty()) {
			int[] tmp = q.poll();
			int r = tmp[0];
			int c = tmp[1];
			for (int i = 0; i < 4; i++) {
				int nr = r + dr[i];
				int nc = c + dc[i];
				if (nr < 0 || nr >= R || nc < 0 || nc >= C) { continue; }
				if (arr[nr][nc] == '#') { continue; }
				if (fireTime[nr][nc] > -1) { continue; }
				fireTime[nr][nc] = fireTime[r][c] + 1;
				q.offer(new int[] {nr, nc});
			}
		}
	}
	
	static void input() throws IOException {
		StringTokenizer st = new StringTokenizer(br.readLine());
		R = Integer.parseInt(st.nextToken());
		C = Integer.parseInt(st.nextToken());
		arr = new char[R][C];
		for (int i = 0; i < R; i++) {
			arr[i] = br.readLine().toCharArray();
		}
		br.close();
	}
	
}
```
