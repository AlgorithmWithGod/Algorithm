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

		int T = Integer.parseInt(br.readLine());
		while(T-- > 0) {
			
			int N = Integer.parseInt(br.readLine());
			int[][] A = new int[N][2];
			for(int i=0;i<N;i++) {
				nextLine();
				A[i][0] = nextInt();
				A[i][1] = nextInt();
			}
			Arrays.sort(A, (a,b) -> {
				if(a[0] == b[0]) return a[1]-b[1];
				return a[0]-b[0];
			});
			
			int[][] ans = new int[N+1][2];
			int num = 1;
			
			int prev = 0;
			
			for(int i=0;i<N;) {
				int x = A[i][0], y = A[i][1], yy = y, p = i;
				while(i<N && x == A[i][0]) {
					yy = A[i][1];
					i++;
				}
				if(y == prev) {
					for(int j=p;j<i;j++) {
						ans[num][0] = A[j][0];
						ans[num][1] = A[j][1];
						num++;
					}
					prev = yy;
				}
				else {
					for(int j=i-1;j>=p;j--) {
						ans[num][0] = A[j][0];
						ans[num][1] = A[j][1];
						num++;
					}
					prev = y;
				}
			}
			
			nextLine();
			int M = nextInt();
			while(M-- > 0) {
				int a = nextInt();
				bw.write(ans[a][0]+" "+ans[a][1]+"\n");
			}
			
		}
		
		bwEnd();
	}

}

```
