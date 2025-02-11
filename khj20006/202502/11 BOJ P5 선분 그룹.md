```java

import java.util.*;
import java.io.*;

class Point{
	int x, y;
	Point(int x, int y){
		this.x = x;
		this.y = y;
	}
	
	public int ccw(Point a, Point b) {
		int x1 = this.x, y1 = this.y;
		int x2 = a.x, y2 = a.y;
		int x3 = b.x, y3 = b.y;
		int res = (x1*y2 + x2*y3 + x3*y1) - (x1*y3 + x2*y1 + x3*y2); 
		return res > 0 ? 1 : (res < 0 ? -1 : 0);
	}
	
}

class Line{
	Point a, b;
	Line(int x1, int y1, int x2, int y2){
		if(x1 < x2 || (x1 == x2 && y1 < y2)) {
			a = new Point(x1,y1);
			b = new Point(x2,y2);			
		}
		else {
			a = new Point(x2,y2);
			b = new Point(x1,y1);
		}
	}
	
	public boolean intersect(Line o) {
		int cond1 = this.a.ccw(this.b, o.a);
		int cond2 = this.b.ccw(this.a, o.b);
		int cond3 = o.a.ccw(o.b, this.a);
		int cond4 = o.b.ccw(o.a, this.b);
		
		
		if(cond1*cond2 < 0 || cond3*cond4 < 0) return false;
		if(cond1*cond2 > 0 && cond3*cond4 > 0) return true;
		if(cond1 == 0) {
			if(this.between(o.a)) return true; 
		}
		if(cond2 == 0) {
			if(this.between(o.b)) return true; 
		}
		if(cond3 == 0) {
			if(o.between(this.a)) return true;
		}
		if(cond4 == 0) {
			if(o.between(this.b)) return true;
		}
		return false;
		
	}
	
	public boolean between(Point p) {
		return this.a.x<=p.x&&p.x<=this.b.x && (this.a.y<=p.y&&p.y<=this.b.y || this.b.y<=p.y&&p.y<=this.a.y);
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
	static Line[] arr;
	static int N;
	static int[] root, cnt;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
	}
	
	static void ready() throws Exception{

		N = Integer.parseInt(br.readLine());
		arr = new Line[N];
		root = new int[N];
		cnt = new int[N];
		for(int i=0;i<N;i++) {
			root[i] = i;
			cnt[i] = 1;
		}
		
		for(int i=0;i<N;i++) {
			nextLine();
			int x1 = nextInt(), y1 = nextInt(), x2 = nextInt(), y2 = nextInt();
			arr[i] = new Line(x1,y1,x2,y2);
		}
		
	}
	
	static void solve() throws Exception{

		for(int i=1;i<N;i++) {
			for(int j=0;j<i;j++) {
				if(arr[i].intersect(arr[j])) {
					int x = f(i), y = f(j);
					if(x != y) {
						cnt[y] += cnt[x];
						root[x] = y;
					}
				}
			}
		}
		
		int ans = 0, max = 0;
		boolean[] vis = new boolean[N];
		for(int i=0;i<N;i++) {
			int x = f(i);
			if(vis[x]) continue;
			vis[x] = true;
			ans++;
			
			if(cnt[x] > max) max = cnt[x];
		}
		bw.write(ans+"\n"+max);
		
	}
	
	static int f(int x) {return x==root[x] ? x : (root[x]=f(root[x]));}
	
}

```
