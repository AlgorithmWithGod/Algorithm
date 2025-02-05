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
	

	
	public static void main(String[] args) throws Exception {

		nextLine();
		int N = nextInt(), A = nextInt(), B = nextInt();
		boolean[][] D = new boolean[N+1][2];
		D[A][0] = true;
		D[B][1] = true;
		
		for(int k=1;k<=20;k++) {
			int d = 1<<(k-1);
			boolean[][] ND = new boolean[N+1][2];
			for(int i=1;i<=N;i++) {
				for(int j=0;j<2;j++) if(D[i][j]) {
					if(i-d > 0) ND[i-d][j] = true;
					if(i+d <= N) ND[i+d][j] = true;					
				}
			}
			for(int i=1;i<=N;i++) {
				D[i][0] = ND[i][0];
				D[i][1] = ND[i][1];
				if(D[i][0] && D[i][1]) {
					bw.write(k+"\n");
					bwEnd();
					return;
				}
			}
		}
		
		
		
		bw.write("-1");

		bwEnd();
	}

}

```
