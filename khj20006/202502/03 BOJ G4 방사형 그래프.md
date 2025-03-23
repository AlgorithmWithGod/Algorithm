```java

import java.util.*;
import java.io.*;

class Point{
	double x, y;
	Point(double x, double y){
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
	static double[] A = new double[8];
	static int ans = 0;
	
	static int ccw(Point a, Point b, Point c) {
		double r = (a.x*b.y + b.x*c.y + c.x*a.y) - (b.x*a.y + c.x*b.y + a.x*c.y);
		return r > 0 ? 1 : (r < 0 ? -1 : 0);
	}
	
	static void sol(int choose, List<Double> arr) {
		if(arr.size() == 8) {
			for(int i=0;i<8;i++) {
				Point a = new Point(0,arr.get(i));
				Point b = new Point(arr.get((i+1)%8) / Math.sqrt(2), arr.get((i+1)%8) / Math.sqrt(2));
				Point c = new Point(arr.get((i+2)%8), 0);
				if(ccw(a,b,c) > 0) return;
			}
			ans++;
			return;
		}
		for(int i=0;i<8;i++) {
			if((choose & (1<<i)) != 0) continue;
			arr.add(A[i]);
			sol(choose | (1<<i), arr);
			arr.remove(arr.size()-1);
		}
	}

	public static void main(String[] args) throws Exception {

		nextLine();
		for(int i=0;i<8;i++) A[i] = nextInt();
		sol(0, new ArrayList<>());
		
		bw.write(ans+"\n");
		
		bwEnd();
	}

}

```
