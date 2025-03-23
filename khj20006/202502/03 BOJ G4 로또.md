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

		long[][] dp = new long[11][2001];
		for(int i=1;i<=2000;i++) dp[1][i] = i;
		for(int i=2;i<=10;i++) {
			for(int j=1;j<=2000;j++) dp[i][j] = dp[i][j-1] + dp[i-1][j/2];
		}
		
		nextLine();
		int T = nextInt();
		
		while(T-- > 0) {
			nextLine();
			int n = nextInt(), m = nextInt();
			bw.write(dp[n][m]+"\n");
		}
		
		bwEnd();
	}

}

```
