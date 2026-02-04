```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.awt.Point;
import java.util.ArrayDeque;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Deque;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class Main {
	private static int T = 0;
	private static int N = 0;
	/*

	 */
	private static List<Point> Points;
	private static Map<Integer, int[]> DpPointsAtX;
	private static boolean[] Visited;
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		Points = new ArrayList<Point>();
		DpPointsAtX = new HashMap<>();

		String[] tokens = br.readLine().split(" ");
		// 0. bfs 큐에 시작지점 추가, 포인트 정렬
		N = Integer.parseInt(tokens[0]);
		T = Integer.parseInt(tokens[1]);
		Visited = new boolean[N];
		int n = N;
		while(n-->0){
			tokens = br.readLine().split(" ");
			Points.add(new Point(Integer.parseInt(tokens[0]), Integer.parseInt(tokens[1])));
		}
		Points.sort((o1, o2) -> o1.x - o2.x);
		Deque<long[]> q = new ArrayDeque<>( );
		q.offer(new long[]{0, 0, 0});
		long answer = 0;
		while(!q.isEmpty()){
		// 1. bfs시작
			long[] qItem = q.poll();
			long x = qItem[0]; long y = qItem[1]; long step = qItem[2];
			if(y == T){
				answer = step;
				break;
			}
			int[] idxBoundOfPointsAtX = getPointsAtX((int) x);
			for(int i = idxBoundOfPointsAtX[0]; i < idxBoundOfPointsAtX[1]; i++){
				int ny = Points.get(i).y;
				if(Math.abs(y - ny)>2){
					continue;
				}
				if(Visited[i]) continue;
				q.offer(new long[]{Points.get(i).x, ny, step+1});
				Visited[i] = true;
			}
		}
		// for(Map.Entry<Integer, int[]> entry : DpPointsAtX.entrySet()){
		// 	System.out.println(entry.getKey() + " : " + Arrays.toString(entry.getValue()));
		// }
		System.out.println((answer != 0)? answer : -1);
		// 2-0. dpPointsAtX에 있는지 확인
		// 2. 현재 시작지점에서 x 차2인것들의 인덱스 범위 추론 -> pointsAtX
		// 3. pointsAtX으로 pointsAtXY 를 구함(O(len(pointsAtX)))
		// 4. dpPointsAtX 에 pointsAtXY를 저장

		br.close();
	}

	private static int[] getPointsAtX(int x) {
		int[] idxsPointsAtX = DpPointsAtX.get(x);
		if(idxsPointsAtX == null){
			//이분탐색으로 구해야함
			int idxOfLowerBound = getLowerBound(x-2);
			int idxOfUppderBound = getUppderBound(x+2);
			//삽입
			DpPointsAtX.putIfAbsent(x, new int[]{idxOfLowerBound, idxOfUppderBound});
			idxsPointsAtX = DpPointsAtX.get(x);
		}
		return idxsPointsAtX;
	}

	private static int getUppderBound(int v) {
		int l = -1; int r = Points.size();
		while(l + 1 < r){
			int mid = (l + r) / 2;
			if(!(Points.get(mid).x > v)) {
				l = mid;
			}else{
				r = mid;
			}
		}
		return r;
	}

	private static int getLowerBound(int v) {
		int l = -1; int r = Points.size();
		while(l + 1 < r){
			int mid = (l + r) / 2;
			if(!(Points.get(mid).x >= v)) {
				l = mid;
			}else{
				r = mid;
			}
		}
		return r;
	}

}
```
