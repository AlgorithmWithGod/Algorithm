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
	static int[][] D, C;
	static int N, P, ans;
	static final int INF = (int)1e9;
	static int start = 0;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = Integer.parseInt(br.readLine());
		D = new int[N][1<<N];
		for(int i=0;i<N;i++) Arrays.fill(D[i], INF);
		C = new int[N][N];
		for(int i=0;i<N;i++) {
		    nextLine();
		    for(int j=0;j<N;j++) C[i][j] = nextInt();
		}
		
		char[] info = br.readLine().toCharArray();
        int temp = 0;
		for(int i=0;i<N;i++) {
            start |= (info[i] == 'Y' ? (1<<i) : 0);
            temp += (info[i] == 'Y' ? 1 : 0);
        }
		
		P = Integer.parseInt(br.readLine());
		for(int i=0;i<N;i++) if((1<<i) != 0) D[i][start] = 0;
		ans = temp >= P ? 0 : INF;
		
	}
	
	static void solve() throws Exception{

		for(int i=0;i<N;i++) dp(i,(1<<N)-1);
		bw.write((ans==INF ? -1 : ans) + "\n");
		
	}
	
	static int dp(int n, int k) throws Exception {
	    if(D[n][k] != INF || (start & (1<<n)) != 0) return D[n][k];
	    int p = k^(1<<n);
	    int prev = INF, cost = INF, cnt = 0;
	    for(int i=0;i<N;i++){
	        if((p & (1<<i)) == 0) continue;
	        cnt++;
	        prev = Math.min(prev, dp(i, p));
	        cost = Math.min(cost, C[i][n]);
	    }
	    D[n][k] = Math.min(D[n][k], prev+cost);
	    if(cnt >= P-1) ans = Math.min(ans, D[n][k]);
	    return D[n][k];
	}
	
}

```
