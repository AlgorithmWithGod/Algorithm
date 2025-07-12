```java
import java.awt.Point;
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayDeque;
import java.util.HashMap;
import java.util.HashSet;
import java.util.StringTokenizer;

public class B7576 {
	private static BufferedReader br;
	private static ArrayDeque<IntAndPoint> q;
	private static StringTokenizer st;
	private static HashSet<Point> wall_tomato_set;
	private static int[][] drdcs = {
			{1, 0},
			{0, -1},
			{-1, 0},
			{0, 1}
	};
	
	private static class IntAndPoint{
		Point p; int level;
		public IntAndPoint(Point p, int level) {
			this.p = p;
			this.level = level;
		}
	}

	public static void main(String[] args) throws IOException {
		br = new BufferedReader(new InputStreamReader(System.in));
		
		//입력
		int n, m;
		String[] temp = br.readLine().split(" ");
		m = Integer.parseInt(temp[0]);
		n = Integer.parseInt(temp[1]);
		q = new ArrayDeque<IntAndPoint>();
		wall_tomato_set = new HashSet<Point>();
		for(int r=0; r<n; r++) {
			st = new StringTokenizer(br.readLine());
			for(int c = 0; c<m; c++) {
				int value = Integer.parseInt(st.nextToken());
				if(value==1) {
					q.add(new IntAndPoint(new Point(r, c), 0));
				}else if(value == -1)
					wall_tomato_set.add(new Point(r, c));
			}
		}
		
		int max_level = 0;
		// bfs 진행
		while(!q.isEmpty()) {
			var temp1 = q.pollFirst();
			Point p = temp1.p;
			wall_tomato_set.add(p);
			int level = temp1.level;
			max_level = Math.max(max_level, level);
			
			for(int[] drdc : drdcs) {
				Point next_p = new Point(p.x + drdc[0], p.y + drdc[1]);
				//범위체크
				if(next_p.x <0 || next_p.x >= n || next_p.y <0 || next_p.y >= m) {
					continue;
				}
				// 벽인지와 토마토인지 확인
				if(wall_tomato_set.contains(next_p))
					continue;
				q.addLast(new IntAndPoint(next_p, level+1));
			}	
		}
		
		// 만약 벽 또는 토마토의 개수가 n*m개수와 다르면 불가능
		if(wall_tomato_set.size() != n*m) {
			System.out.println(-1);
		}else {
			System.out.println(max_level);
		}
		br.close();
	}

}
```
