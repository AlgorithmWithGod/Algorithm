```java

import java.util.*;
import java.io.*;


class Main {
	
	// IO field
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
	static StringTokenizer st = new StringTokenizer("");

	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() throws Exception {
		if(!st.hasMoreTokens()) nextLine();
		return Integer.parseInt(st.nextToken());
	}
	static long nextLong() throws Exception {
		if(!st.hasMoreTokens()) nextLine();
		return Long.parseLong(st.nextToken());
	}
	static void bwEnd() throws Exception {bw.flush();bw.close();}
	
	// Additional field
	
	static final int INF = 1000111777;
	
	static int N, M, L, G;
	static int[][] right, down;
	static int[][][][] D;
	
	
	public static void main(String[] args) throws Exception {
		
		for(int T=nextInt();T-->0;) {
			
			ready();
			solve();
		}
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = nextInt();
		M = nextInt();
		L = nextInt();
		G = nextInt();
		right = new int[N][M];
		down = new int[N][M];
		D = new int[N][M][Math.min(N-1, M-1)*2+2][2];
		
		for(int i=0;i<N;i++) for(int j=0;j<M-1;j++) right[i][j] = nextInt();
		for(int i=0;i<N-1;i++) for(int j=0;j<M;j++) down[i][j] = nextInt();
		
	}
	
	static void solve() throws Exception{
		
		dp();
		int ans = INF;
		for(int i=0;i<Math.min(N-1, M-1)*2+2;i++) {
			if(Math.min(D[N-1][M-1][i][0], D[N-1][M-1][i][1]) <= G) {
				bw.write((L*(N+M-2)+i)+"\n");
				return;
			}
		}
		bw.write("-1\n");
		
	}
	
	static void dp() {
		
		for(int i=0;i<N;i++) for(int j=0;j<M;j++) for(int k=0;k<Math.min(N-1,M-1)*2+2;k++) Arrays.fill(D[i][j][k], INF);
		
		D[0][1][0][0] = right[0][0];
		D[1][0][0][1] = down[0][0];
		for(int i=0;i<N;i++) for(int j=0;j<M;j++) for(int k=0;k<Math.min(N-1, M-1)*2+2;k++) {
			if(i+j <= 1) continue;
			if(j>0) {
				D[i][j][k][0] = right[i][j-1];
				int res = D[i][j-1][k][0];
				if(k > 0) res = Math.min(res, D[i][j-1][k-1][1]);
				D[i][j][k][0] += res;
			}
			if(i>0) {
				D[i][j][k][1] = down[i-1][j];
				int res = D[i-1][j][k][1];
				if(k > 0) res = Math.min(res, D[i-1][j][k-1][0]);
				D[i][j][k][1] += res;
			}
		}
		
	}
	
}

```
