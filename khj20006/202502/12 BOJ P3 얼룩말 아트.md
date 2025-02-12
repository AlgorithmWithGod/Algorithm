```java

import java.util.*;
import java.io.*;

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
	static int[][] SQ, arr;
	static int W, H, K;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
	}
	
	static void ready() throws Exception{

		nextLine();
		H = nextInt();
		W = nextInt();
		K = nextInt();
		SQ = new int[W+2][H+2];
		arr = new int[W+2][H+2];
		
	}
	
	static void solve() throws Exception{

		while(K-- > 0) {
			nextLine();
			int op = nextInt(), py = nextInt(), px = nextInt();
			px++;
			py++;
			if(op == 1) {
				int qy = nextInt(), qx = nextInt();
				qx++;
				qy++;
				Square(px,py,qx,qy);
			}
			else {
				int r = nextInt();
				if(r == 1) {
					arr[px][py]++;
					arr[px+1][py]++;
					arr[px-1][py]++;
					arr[px][py+1]++;
					arr[px][py-1]++;
				}
				else {
					RightUp(px-1,py+1,r-2);
					RightDown(px+1,py+1,r-2);
					LeftUp(px-1,py-1,r-2);
					LeftDown(px+1,py-1,r-2);
					Square(px-r,py,px+r,py);
					Square(px,py-r,px,py+r);
					arr[px][py]--;
				}
			}
		}
		
		for(int i=1;i<=W;i++) {
			int s = 0;
			for(int j=1;j<=H;j++) {
				SQ[i+1][j] += SQ[i][j];
				s += SQ[i][j];
				arr[i][j] += s;
				bw.write(arr[i][j]%2 == 0 ? '.' : '#');
			}
			bw.write("\n");
		}
		
		
	}
	
	static void Square(int px, int py, int qx, int qy) {
		SQ[px][py]++;
		SQ[qx+1][py]--;
		SQ[px][qy+1]--;
		SQ[qx+1][qy+1]++;
	}
	
	static void RightUp(int x, int y, int r) {
		if(r == 0) {
			arr[x][y]++;
			return;
		}
		if(r == 1) {
			arr[x][y]++;
			arr[x-1][y]++;
			arr[x][y+1]++;
			return;
		}
		int nr = r/2;
		Square(x-nr,y,x,y+nr);
		RightUp(x-nr-1,y,(r-1)/2);
		RightUp(x,y+nr+1,(r-1)/2);
	}
	
	static void RightDown(int x, int y, int r) {
		if(r == 0) {
			arr[x][y]++;
			return;
		}
		if(r == 1) {
			arr[x][y]++;
			arr[x+1][y]++;
			arr[x][y+1]++;
			return;
		}
		int nr = r/2;
		Square(x,y,x+nr,y+nr);
		RightDown(x+nr+1,y,(r-1)/2);
		RightDown(x,y+nr+1,(r-1)/2);
	}
	
	static void LeftUp(int x, int y, int r) {
		if(r == 0) {
			arr[x][y]++;
			return;
		}
		if(r == 1) {
			arr[x][y]++;
			arr[x-1][y]++;
			arr[x][y-1]++;
			return;
		}
		int nr = r/2;
		Square(x-nr,y-nr,x,y);
		LeftUp(x-nr-1,y,(r-1)/2);
		LeftUp(x,y-nr-1,(r-1)/2);
	}
	
	static void LeftDown(int x, int y, int r) {
		if(r == 0) {
			arr[x][y]++;
			return;
		}
		if(r == 1) {
			arr[x][y]++;
			arr[x+1][y]++;
			arr[x][y-1]++;
			return;
		}
		int nr = r/2;
		Square(x,y-nr,x+nr,y);
		LeftDown(x+nr+1,y,(r-1)/2);
		LeftDown(x,y-nr-1,(r-1)/2);
	}
	
}

```
