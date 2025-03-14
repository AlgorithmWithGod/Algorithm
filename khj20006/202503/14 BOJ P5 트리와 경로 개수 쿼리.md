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
	
	static int N;
	static int[] A;
	static long[] R, B, ans;
	static List<Integer>[] V;
	static long blue = 0, red = 0;
	
	public static void main(String[] args) throws Exception {
			
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = nextInt();
		A = new int[N+1];
		for(int i=1;i<=N;i++) {
			A[i] = nextInt();
			red += A[i] == 1 ? 1 : 0;
			blue += A[i] == 0 ? 1 : 0;
		}
		V = new List[N+1];
		for(int i=1;i<=N;i++) V[i] = new ArrayList<>();
		
		for(int i=1;i<N;i++) {
			int a = nextInt(), b = nextInt();
			V[a].add(b);
			V[b].add(a);
		}
		
		R = new long[N+1];
		B = new long[N+1];
		ans = new long[N+1];
		
	}
	
	static void solve() throws Exception{
		
		dfs(1, 0);
		for(int Q=nextInt();Q-->0;) {
			int x = nextInt();
			bw.write(ans[x] + "\n");
		}
		
	}
	
	static void dfs(int n, int p) {
		
		for(int i:V[n]) if(i != p) {
			dfs(i, n);
			R[n] += R[i] + (A[i] == 1 ? 1 : 0);
			B[n] += B[i] + (A[i] == 0 ? 1 : 0);
		}
		ans[n] += R[n] * (blue - (B[n] + (A[n] == 0 ? 1 : 0)));
		ans[n] += B[n] * (red - (R[n] + (A[n] == 1 ? 1 : 0)));
		for(int i:V[n]) if(i != p) {
			ans[n] += (R[i] + (A[i] == 1 ? 1 : 0)) * (B[n] - (B[i] + (A[i] == 0 ? 1 : 0)));
		}
		
	}
	
}

```
