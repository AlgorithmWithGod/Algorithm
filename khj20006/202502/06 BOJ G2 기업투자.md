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
	
	static int N, M;
	static int[][] A;
	static int[] D;
	static int[][] R;

	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
		
		bwEnd();
	}
	
	static void ready() throws Exception{

		nextLine();
		N = nextInt();
		M = nextInt();
		A = new int[N+1][M+1];
		D = new int[N+1];
		R = new int[N+1][N+1];
		
		for(int i=1;i<=N;i++) {
			nextLine();
			nextInt();
			for(int j=1;j<=M;j++) A[i][j] = nextInt();
		}
		
	}
	
	static void solve() throws Exception{

		for(int i=1;i<=M;i++) {
			int[] ND = new int[N+1];
			int[][] NR = new int[N+1][N+1];
			for(int n=1;n<=N;n++) {
				ND[n] = A[n][i];
				NR[n][i] = n;
				for(int k=1;k<n;k++) {
					int res = D[k] + A[n-k][i];
					if(res > ND[n]) {
						ND[n] = res;
						for(int j=1;j<i;j++) NR[n][j] = R[k][j];
						NR[n][i] = n-k;
					}
				}
			}
			for(int n=1;n<=N;n++) {
				if(ND[n] > D[n]) {
					D[n] = ND[n];
					R[n] = NR[n];
				}
			}
		}
		
		bw.write(D[N] + "\n");
		for(int i=1;i<=M;i++) bw.write(R[N][i] + " ");
		
	}

	
}

```
