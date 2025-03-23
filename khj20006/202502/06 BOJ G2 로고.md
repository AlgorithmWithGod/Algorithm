import java.util.*;
import java.io.*;

class Rect{
	int x, y, w, h;
	Rect(int x, int y, int w, int h){
		this.x = x;
		this.y = y;
		this.w = w;
		this.h = h;
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
	
	
	static Rect[] arr;
	static int N;
	static int[] r;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
		
		bwEnd();
	}
	
	static void ready() throws Exception{

		N = Integer.parseInt(br.readLine());
		r = new int[N+1];
		for(int i=0;i<=N;i++) r[i] = i;
		arr = new Rect[N+1];
		arr[0] = new Rect(0,0,0,0);
		for(int i=1;i<=N;i++) {
			nextLine();
			int x1 = nextInt();
			int y1 = nextInt();
			int x2 = nextInt();
			int y2 = nextInt();
			arr[i] = new Rect(x1, y1, x2-x1, y2-y1);
		}
		
	}
	
	static void solve() throws Exception{

		for(int i=1;i<=N;i++) {
			for(int j=0;j<i;j++) {
				if(!intersect(arr[i],arr[j])) continue;
				int x = f(i), y = f(j);
				if(x == y) continue;
				r[x] = y;
			}
		}
		
		int ans = 0;
		boolean vis[] = new boolean[N+1];
		vis[f(0)] = true;
		for(int i=1;i<=N;i++) {
			int x = f(i);
			if(!vis[x]) {
				vis[x] = true;
				ans++;
			}
		}
		
		bw.write(ans+"\n");
		
	}
	
	static boolean intersect(Rect a, Rect b) {
		if(a.x + a.w < b.x) return false;
		if(b.x + b.w < a.x) return false; 
		if(a.y + a.h < b.y) return false;
		if(b.y + b.h < a.y) return false;
		if((a.x < b.x && b.x + b.w < a.x + a.w) && (a.y < b.y && b.y + b.h < a.y + a.h)) return false;
		if((b.x < a.x && a.x + a.w < b.x + b.w) && (b.y < a.y && a.y + a.h < b.y + b.h)) return false;
		return true;
	}

	static int f(int x) {return x==r[x] ? x : (r[x]=f(r[x]));}
	
}
