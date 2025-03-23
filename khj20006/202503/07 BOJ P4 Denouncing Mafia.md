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

	static int N, K;
	static List<Integer>[] V;
	static int[] C;
	
	public static void main(String[] args) throws Exception {
			
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		nextLine();
		N = nextInt();
		K = nextInt();
		
		V = new List[N+1];
		C = new int[N+1];
		for(int i=1;i<=N;i++) V[i] = new ArrayList<>();
		
		nextLine();
		for(int i=2;i<=N;i++) V[nextInt()].add(i);
		
	}
	
	static void solve() throws Exception{
		
		int ans = 0;
		for(int x = dfs(1);K > 0 && x >= 1;) {
			if(C[x] > 0) {
				C[x]--;
				ans += x;
				K--;
			}
			else x--;
		}
		
		bw.write(ans + "\n");
		
	}
	
	static int dfs(int n) {
		int mx = 0;
		for(int i:V[n]) mx = Math.max(mx, dfs(i));
		C[mx++]--;
		C[mx]++;
		return mx;
	}
	
}

```
