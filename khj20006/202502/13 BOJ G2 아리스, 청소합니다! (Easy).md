```java

import java.util.*;
import java.io.*;

class Node {
	int x, y, dir, time;
	Node(int x, int y, int dir, int time){
		this.x = x;
		this.y = y;
		this.dir = dir;
		this.time = time;
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
	static int[] dx = {-1,0,1,0};
	static int[] dy = {0,1,0,-1};
	static int H, W, R, C, D;
	
	static int[][] A, B;
	static boolean[][] dust;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
	}
	
	static void ready() throws Exception{
		
		nextLine();
		H = nextInt();
		W = nextInt();
		nextLine();
		R = nextInt();
		C = nextInt();
		D = nextInt();
		
		A = new int[H][W];
		B = new int[H][W];
		for(int i=0;i<H;i++) {
			char[] arr = br.readLine().toCharArray();
			for(int j=0;j<W;j++) A[i][j] = arr[j]-'0';
		}
		for(int i=0;i<H;i++) {
			char[] arr = br.readLine().toCharArray();
			for(int j=0;j<W;j++) B[i][j] = arr[j]-'0';
		}
		
		dust = new boolean[H][W];
	}
	
	static void solve() throws Exception{

		int time = 0, ans = 0;
		while(time <= 100000000) {
			
			boolean wasDust = !dust[R][C];

			int PS = dust[R][C] ? B[R][C] : A[R][C];
			D = (D + PS) % 4;
			dust[R][C] = true;
			R += dx[D];
			C += dy[D];
			time++;
			if(wasDust) ans = time;
			if(out(R,C)) break;
			
		}
		bw.write(ans + "\n");
	}
	
	static boolean out(int x, int y) {
		return x<0 || x>=H || y<0 || y>=W;
	}
	
}

```
