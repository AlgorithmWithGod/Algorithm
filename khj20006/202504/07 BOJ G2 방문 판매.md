```java

import java.util.*;
import java.io.*;

class Main {
	
	// IO field
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
	static StringTokenizer st = new StringTokenizer("");

	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static String nextToken() throws Exception {
		while(!st.hasMoreTokens()) nextLine();
		return st.nextToken();
	}
	static int nextInt() throws Exception { return Integer.parseInt(nextToken()); }
	static long nextLong() throws Exception { return Long.parseLong(nextToken()); }
	static double nextDouble() throws Exception { return Double.parseDouble(nextToken()); }
	static void bwEnd() throws Exception {bw.flush();bw.close();}
	
	// Additional field
	
	static int N, X, Y;
	static int[] x, y;
	static int[][] max, rec;
	
	static final int INF = -123456;
	
	public static void main(String[] args) throws Exception {
			
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = nextInt();
		X = nextInt();
		Y = nextInt();
		x = new int[N];
		y = new int[N];
		for(int i=0;i<N;i++) {
			x[i] = nextInt();
			y[i] = nextInt();
		}
		max = new int[5001][51];
		rec = new int[5001][51];
		for(int i=0;i<=5000;i++) {
			Arrays.fill(max[i], INF);
			Arrays.fill(rec[i], INF);
		}
		
	}
	
	static void solve() throws Exception{
		
		max[0][0] = 0;
		for(int i=0;i<N;i++) {
			for(int c=i+1;c>0;c--) for(int j=100*(i+1);j>=x[i];j--) if(max[j-x[i]][c-1] != INF) {
				if(max[j][c] < Y && max[j-x[i]][c-1] + y[i] >= Y) {
					rec[j][c] = i+1;
				}
				max[j][c] = Math.max(max[j][c], max[j-x[i]][c-1] + y[i]);
			}
		}
		
		for(int c=1;c<=N;c++) {
			boolean find = false;
			int min = -INF;
			for(int i=X;i<=5000;i++) if(max[i][c] >= Y) {
				find = true;
				min = Math.min(min, rec[i][c]);
			}
			if(find) {
				bw.write(c + "\n" + min);
				return;
			}
		}
		bw.write("-1");
		
	}
	
}

```
