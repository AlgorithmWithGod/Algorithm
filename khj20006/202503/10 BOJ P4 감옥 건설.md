```java

import java.util.*;
import java.io.*;

class Point{
	int x,y,id;
	Point(int x, int y, int id){
		this.x = x;
		this.y = y;
		this.id = id;
	}
	
	// this -> a -> b CCW
	// 1 : CCW, 0 : line, 1 : CW
	int ccw(Point a, Point b) {
		long res = (long)a.x * b.y + (long)b.x * this.y + (long)this.x * a.y - ((long)b.x * a.y + (long)this.x * b.y + (long)a.x * this.y);
		if(res == 0) return 0;
		return res > 0 ? 1 : -1;
	}
	boolean isInPolygon(List<Point> A) {
		if(A.size() < 3) return false;
		boolean res = true;
		for(int i=0;i<A.size();i++) {
			Point cur = A.get(i), next = A.get((i+1)%A.size());
			res &= this.ccw(cur, next) == 1;
		}
		return res;
	}
}

class Main {
	
	// IO field
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
	static StringTokenizer st;

	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	static long nextLong() {return Long.parseLong(st.nextToken());}
	static void bwEnd() throws Exception {bw.flush();bw.close();}
	
	// Additional field

	static int N;
	static Point prison;
	static Point[] walls;
	static boolean[] used;
	
	public static void main(String[] args) throws Exception {
			
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		nextLine();
		N = nextInt();
		prison = new Point(nextInt(), nextInt(), -1);
		walls = new Point[N];
		used = new boolean[N];
		for(int i=0;i<N;i++) {
			nextLine();
			walls[i] = new Point(nextInt(), nextInt(), -1);
		}
		Arrays.sort(walls, (a,b) -> {
			if(a.x == b.x) return a.y-b.y;
			return a.x-b.x;
		});
		for(int i=0;i<N;i++) walls[i].id = i;
		
	}
	
	static void solve() throws Exception{
		
		int ans = 0;
		while(canConstructConvexHull()) ans++;
		bw.write(ans + "\n");
		
	}
	
	static boolean canConstructConvexHull() throws Exception {
		
		List<Point> lower = new ArrayList<>();
		List<Point> upper = new ArrayList<>();
		for(int i=0;i<N;i++) if(!used[i]) {
			while(lower.size() > 1 && walls[i].ccw(lower.get(lower.size()-2), lower.get(lower.size()-1)) <= 0) lower.remove(lower.size()-1);
			while(upper.size() > 1 && walls[i].ccw(upper.get(upper.size()-2), upper.get(upper.size()-1)) >= 0) upper.remove(upper.size()-1);
			lower.add(walls[i]);
			upper.add(walls[i]);
		}
		
		List<Point> convexHull = new ArrayList<>();
		for(int i=0;i<lower.size();i++) {
			used[lower.get(i).id] = true;
			convexHull.add(lower.get(i));
			
		}
		for(int i=upper.size()-2;i>0;i--) {
			used[upper.get(i).id] = true;
			convexHull.add(upper.get(i));
		}
		
		
		return prison.isInPolygon(convexHull);
		
	}
	
}

```
