```java

import java.util.*;
import java.io.*;

class Point{
	long x,y;
	Point(long x, long y){
		this.x = x;
		this.y = y;
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
	static Point[] arr;
	static Point[] convexHull;
	
	
	static int N;
	static long ans = 0;
	
	// positive : ccw
	static int ccw(Point a, Point b, Point c) {
		long res = (a.x*b.y + b.x*c.y + c.x*a.y) - (b.x*a.y + c.x*b.y + a.x*c.y);
		if(res > 0) return 1;
		if(res < 0) return -1;
		return 0;
	}
	
	public static void main(String[] args) throws Exception {

		input();
		
		if(N <= 2) {
			if(N == 1) bw.write("0");
			else {
				long dx = arr[0].x - arr[1].x;
				long dy = arr[0].y - arr[1].y;
				bw.write((dx*dx+dy*dy) + "\n");
			}
			bwEnd();
			return;
		}
		
		constructConvexHull();
		
		rotate();
		
		bw.write(ans+"\n");

		bwEnd();
	}
	
	static void input() throws Exception {
		nextLine();
		N = nextInt();
		arr = new Point[N];
		for(int i=0;i<N;i++) {
			nextLine();
			arr[i] = new Point(nextLong(), nextLong());
		}
	}
	
	static void constructConvexHull() {
		
		Arrays.sort(arr, (a,b) -> {
			if(a.x==b.x) return (int)(a.y-b.y);
			return (int)(a.x-b.x);
		});
		List<Point> lowerHull = new ArrayList<>();
		List<Point> upperHull = new ArrayList<>();
		for(Point p : arr) {
			while(lowerHull.size()>1 && ccw(lowerHull.get(lowerHull.size()-2), lowerHull.get(lowerHull.size()-1), p) <= 0) lowerHull.remove(lowerHull.size()-1);
			lowerHull.add(p);
			while(upperHull.size()>1 && ccw(upperHull.get(upperHull.size()-2), upperHull.get(upperHull.size()-1), p) >= 0) upperHull.remove(upperHull.size()-1);
			upperHull.add(p);
		}
		
		convexHull = new Point[lowerHull.size() + upperHull.size() - 2];
		int idx = 0;
		for(Point p : upperHull) convexHull[idx++] = p;
		idx--;
		for(int i=lowerHull.size()-1;i>0;i--) convexHull[idx++] = lowerHull.get(i);
		
	}
	
	static void rotate() {
		int p = 1, sz = convexHull.length;
		for(int i=0;i<sz;i++) {
			long dx = convexHull[p%sz].x - convexHull[(i+1)%sz].x;
			long dy = convexHull[p%sz].y - convexHull[(i+1)%sz].y;
			ans = Math.max(ans, dist(convexHull[i],convexHull[p%sz]));
			while(p < 2*sz && ccw(convexHull[i], convexHull[(i+1)%sz], new Point(convexHull[(p+1)%sz].x - dx, convexHull[(p+1)%sz].y - dy)) <= 0) {
				p++;
				ans = Math.max(ans, dist(convexHull[i],convexHull[p%sz]));
				dx = convexHull[p%sz].x - convexHull[(i+1)%sz].x;
				dy = convexHull[p%sz].y - convexHull[(i+1)%sz].y;
			}
		}
	}
	
	static long dist(Point a, Point b) {
		return (a.x-b.x)*(a.x-b.x) + (a.y-b.y)*(a.y-b.y);
	}
	
}

```
