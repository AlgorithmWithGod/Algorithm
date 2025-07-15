```java
import java.awt.Point;
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayDeque;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.HashMap;
import java.util.HashSet;
import java.util.Iterator;
import java.util.LinkedList;import java.util.Map;
import java.util.StringTokenizer;

public class B15683 {
	static class CCTV{
		int id;
		Point p;
		public CCTV(int id, Point p) {
			this.id = id;
			this.p = p;
		}
	}
	private static BufferedReader br;
	private static int m;
	private static int n;
	private static LinkedList<int[]> combinations;
	private static int[] comb;
	private static ArrayList<B15683.CCTV> cctvs;
	private static HashSet<Point> walls;
	private static ArrayDeque<Point> buffer;
	private static int[][] drdcs = {
			{0, 1},{1, 0},{0, -1}, {-1, 0}
	};
	private static int[][][] indexesDrdcsAtId = {null, {{0}, {1}, {2}, {3}}
	,{{0, 2}, {1, 3}, {0, 2}, {1, 3}}
	,{{0, 1}, {1, 2}, {2, 3}, {3, 0}}
	,{{0, 1, 2}, {1, 2, 3}, {2, 3, 0}, {3, 0, 1}}
	,{{0, 1, 2, 3}, {0, 1, 2, 3}, {0, 1, 2, 3}, {0, 1, 2, 3}}};
	private static int[][] map;
	public static void main(String[] args) throws IOException {
		br = new BufferedReader(new InputStreamReader(System.in));
		var tokens = br.readLine().split(" ");
		n = Integer.parseInt(tokens[0]);
		m = Integer.parseInt(tokens[1]);
		walls = new HashSet<Point>();
		cctvs = new ArrayList<CCTV>();
		map = new int[n][m];
		for(int r = 0; r<n; r++) {
			var st = new StringTokenizer(br.readLine());
			for(int c = 0; c<m; c++) {
				String value = st.nextToken();
				int valueInt = Integer.parseInt(value);
				map[r][c] = valueInt;
				if("0".equals(value))
					continue;
				if("6".equals(value)) {
					walls.add(new Point(r, c));
				}else {
					cctvs.add(new CCTV(valueInt, new Point(r, c)));
				}
			}
		}
		
		int nOfZero = n*m - walls.size() - cctvs.size();
		int answer = nOfZero;
		for (Iterator iterator = getCombinations().iterator(); iterator.hasNext();) {
			buffer = new ArrayDeque<Point>();
			int[] directions = (int[]) iterator.next();
			
			for(int i = 0; i<directions.length; i++) {
				int direction = directions[i];
				//cctvs[i]에서의 direction을 기준으로 map반영
				fetchMap(cctvs.get(i), direction);
				//printMap();
			}
			answer = Math.min(answer, nOfZero - buffer.size());
			recoverMap();
		}
		System.out.println(answer);
		
	}

	private static void printMap() {
		for (int r = 0; r < map.length; r++) {
			for (int c = 0; c < map[0].length; c++) {
				System.out.print(map[r][c] + " ");
			}
			System.out.println();
		}
		System.out.println("------");
	}

	private static void recoverMap() {
		while(!buffer.isEmpty()) {
			Point p = buffer.pollLast();
			map[p.x][p.y] = 0;
		}
		
	}

	private static void fetchMap(CCTV cctv, int direction) {
		for(int idDrdcs : indexesDrdcsAtId[cctv.id][direction]){
			int[] drdc = drdcs[idDrdcs];
			int nr = cctv.p.x;
			int nc = cctv.p.y;
			
			while(true) {
				nr+= drdc[0];
				nc+= drdc[1];
				if((nr<0 || nr >= n || nc <0 || nc>=m) || walls.contains(new Point(nr, nc))) {
					break;
				}
				if(map[nr][nc] >= 1 && map[nr][nc] <= 5)
					continue;
				map[nr][nc] = cctv.id;
				buffer.addLast(new Point(nr, nc));
			}
			
		}
	}

	private static LinkedList<int[]> getCombinations() {
		combinations = new LinkedList<int[]>();
		comb = new int[cctvs.size()]; 
		recur(0);
		
		return combinations;
	}

	private static void recur(int index) {
		if(index == cctvs.size()) {
			combinations.add(comb.clone());
			return;
		}
		for(int i = 0; i<4; i++) {
			comb[index] = i;
			recur(index+1);
		}
		
	}

}
```
