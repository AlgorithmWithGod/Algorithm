```java

import java.util.*;
import java.io.*;

class Point{
	long x,y;
	Point(long x, long y){
		this.x = x;
		this.y = y;
	}
	/*
	 * 1  : 반시계
	 * -1 : 시계
	 * 0  : 직선 
	 */
	int ccw(Point p, Point q) {
		long res = p.x * q.y + q.x * this.y + this.x * p.y - (q.x * p.y + this.x * q.y + p.x * this.y);
		if(res > 0) return 1;
		if(res < 0) return -1;
		return 0;
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

	static int N, M, K;
	static Point[] A, B, L;
	static List<Point> lowerA;
	static List<Point> upperA;
	static List<Point> lowerB;
	static List<Point> upperB;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		nextLine();
		N = nextInt();
		M = nextInt();
		K = nextInt();
		A = new Point[N];
		B = new Point[M];
		L = new Point[K];
		
		nextLine();
		for(int i=0;i<N;i++) A[i] = new Point(nextInt(), nextInt());
		
		nextLine();
		for(int i=0;i<M;i++) B[i] = new Point(nextInt(), nextInt());
		
		nextLine();
		for(int i=0;i<K;i++) L[i] = new Point(nextInt(), nextInt());
		
	}
	
	static void solve() throws Exception{
		
		List<Point>[] resA = splitConvexHull(A);
		lowerA = resA[0];
		upperA = resA[1];
		
		List<Point>[] resB = splitConvexHull(B);
		lowerB = resB[0];
		upperB = resB[1];
		
//		bw.write("A's Lower Hull ===========\n");
//		for(Point temp:lowerA) bw.write("(" + temp.x + "," + temp.y + ") -> ");
//		bw.write("\n");
//		bw.write("A's Upper Hull ===========\n");
//		for(Point temp:upperA) bw.write("(" + temp.x + "," + temp.y + ") -> ");
//		bw.write("\n");
//		bw.write("B's Lower Hull ===========\n");
//		for(Point temp:lowerB) bw.write("(" + temp.x + "," + temp.y + ") -> ");
//		bw.write("\n");
//		bw.write("B's Upper Hull ===========\n");
//		for(Point temp:upperB) bw.write("(" + temp.x + "," + temp.y + ") -> ");
//		bw.write("\n");
		
		
		int cntA = 0, cntB = 0;
		for(Point now:L) {
			
			boolean isInsideA = false;
			boolean isInsideB = false;
			
			// A의 내부에 있는지
			long minX = lowerA.get(0).x, maxX = lowerA.get(lowerA.size()-1).x;
			if(minX < now.x && now.x < maxX) {
				isInsideA = true;
				int idx1 = findLowerBound(lowerA, now.x);
				
				if(idx1-1 >= 0 && idx1 < lowerA.size()) isInsideA &= (now.ccw(lowerA.get(idx1-1), lowerA.get(idx1)) == 1);
				if(idx1 >= 0 && idx1+1 < lowerA.size()) isInsideA &= (now.ccw(lowerA.get(idx1), lowerA.get(idx1+1)) == 1);
				if(idx1+1 >= 0 && idx1+2 < lowerA.size()) isInsideA &= (now.ccw(lowerA.get(idx1+1), lowerA.get(idx1+2)) == 1);
				
				int idx2 = findLowerBound(upperA, now.x);
				
				
				if(idx2+1 < upperA.size()) isInsideA &= (now.ccw(upperA.get(idx2+1), upperA.get(idx2)) == 1);
				if(idx2-1 >= 0 && idx2 < upperA.size()) isInsideA &= (now.ccw(upperA.get(idx2), upperA.get(idx2-1)) == 1);
				if(idx2-2 >= 0 && idx2-1 < upperA.size()) isInsideA &= (now.ccw(upperA.get(idx2-1), upperA.get(idx2-2)) == 1);
				
				if(isInsideA) cntA++;
			}
			
			// B의 내부에 있는지
			minX = lowerB.get(0).x;
			maxX = lowerB.get(lowerB.size()-1).x;
			if(minX < now.x && now.x < maxX) {
				isInsideB = true;
				int idx1 = findLowerBound(lowerB, now.x);
				
				if(idx1 < lowerB.size() && idx1-1 >= 0) isInsideB &= (now.ccw(lowerB.get(idx1-1), lowerB.get(idx1)) == 1);
				if(idx1 >= 0 && idx1+1 < lowerB.size()) isInsideB &= (now.ccw(lowerB.get(idx1), lowerB.get(idx1+1)) == 1);
				if(idx1+2 < lowerB.size()) isInsideB &= (now.ccw(lowerB.get(idx1+1), lowerB.get(idx1+2)) == 1);
				
				int idx2 = findLowerBound(upperB, now.x);
				
				if(idx2+1 < upperB.size()) isInsideB &= (now.ccw(upperB.get(idx2+1), upperB.get(idx2)) == 1);
				if(idx2-1 >= 0 && idx2 < upperB.size()) isInsideB &= (now.ccw(upperB.get(idx2), upperB.get(idx2-1)) == 1);
				if(idx2-2 >= 0 && idx2-1 < upperB.size()) isInsideB &= (now.ccw(upperB.get(idx2-1), upperB.get(idx2-2)) == 1);
				
				if(isInsideB) cntB++;
			}
			
//			bw.write("(" + now.x + "," + now.y + ") is " + (isInsideA ? "inside of A\n" : "not inside of A\n"));
//			bw.write("(" + now.x + "," + now.y + ") is " + (isInsideB ? "inside of B\n" : "not inside of B\n"));
			
		}
		
		
		int ans = K-cntA+cntB;
		if(ans == 0) bw.write("YES\n");
		else bw.write(ans + "\n");
		
	}
	
	static List<Point>[] splitConvexHull(Point[] P) {
		List<Point> lower = new ArrayList<>();
		List<Point> upper = new ArrayList<>();
		
		long minX = (long)2e9, maxX = -(long)2e9;
		int idxLower = -1, idxUpper = -1;
		for(int i=0;i<P.length;i++) {
			if(P[i].x <= minX) {
				minX = P[i].x;
				idxLower = i;
			}
			if(P[i].x >= maxX) {
				maxX = P[i].x;
				idxUpper = i;
			}
		}
		
		if(idxUpper < idxLower) idxUpper += P.length;
		for(int i=idxLower;i<=idxUpper;i++) lower.add(P[i%P.length]);
		for(int i=idxLower+P.length;i>=idxUpper;i--) upper.add(P[i%P.length]);
		
		return new List[] {lower,upper};
	}
	
	static int findLowerBound(List<Point> list, long x) {
		
		int s = 0, e = list.size(), m = (s+e)>>1;
		while(s<e) {
			long temp = list.get(m).x;
			if(temp < x) s = m+1;
			else e = m;
			m = (s+e)>>1;
		}
		return m;
		
	}
	
}

```
