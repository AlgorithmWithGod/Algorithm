```java

import java.util.*;
import java.io.*;

class Edge{
	int x;
	long c;
	Edge(int x, long c){
		this.x = x;
		this.c = c;
	}
}

class Element {
	long dist, cnt;
	int node;
	Element(long dist, long cnt, int node){
		this.dist = dist;
		this.cnt = cnt;
		this.node = node;
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
	static long[] dp;
	static int[] A;
	static int N, M;
	
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
		
		bwEnd();
	}
	
	static void ready() throws Exception{

		nextLine();
		N = nextInt();
		M = nextInt();
		dp = new long[M+1];
		Arrays.fill(dp, -1);
		A = new int[N];
		for(int i=0;i<N;i++) A[i] = Integer.parseInt(br.readLine());
		
	}
	
	static void solve() throws Exception{
		
		dp[A[0]] = 0;
		for(int i=1;i<N;i++) {
			long[] ndp = new long[M+1];
			Arrays.fill(ndp, -1);
			for(int j=1;j<=M;j++) {
				if(dp[j] != -1) {
					if(j + 1 + A[i] <= M) {
						if(ndp[j+1+A[i]] == -1) ndp[j+1+A[i]] = dp[j];
						else ndp[j+1+A[i]] = Math.min(ndp[j+1+A[i]], dp[j]);
					}
					if(ndp[A[i]] == -1) ndp[A[i]] = dp[j] + (M-j)*(M-j);
					else ndp[A[i]] = Math.min(ndp[A[i]], dp[j] + (M-j)*(M-j));
				}
			}
			dp = ndp;
		}
		
		long ans = Long.MAX_VALUE;
		for(int i=1;i<=M;i++) if(dp[i] != -1) ans = Math.min(ans, dp[i]);
		bw.write(ans+"\n");
		
	}
	
}

```
