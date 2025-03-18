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
		if(!st.hasMoreTokens()) nextLine();
		return st.nextToken();
	}
	static int nextInt() throws Exception { return Integer.parseInt(nextToken()); }
	static long nextLong() throws Exception { return Long.parseLong(nextToken()); }
	static void bwEnd() throws Exception {bw.flush();bw.close();}
	
	// Additional field
	
	static int N;
	static List<Integer>[] V;
	static int[] D;
	static int ans = 0;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = nextInt();
		D = new int[N+1];
		V = new List[N+1];
		for(int i=1;i<=N;i++) V[i] = new ArrayList<>();
		for(int i=1;i<N;i++) {
			int a = nextInt(), b = nextInt();
			V[a].add(b);
			V[b].add(a);
			D[a]++;
			D[b]++;
		}
		
	}
	
	static void solve() throws Exception{
		
		for(int i=1;i<=N;i++) if(D[i] > 3) {
			bw.write("-1");
			return;
		}
		
		for(int i=1;i<=N;i++) {
			if(D[i] == 2) {
				dfs(i,0);
				bw.write(ans + "\n");
				return;
			}
		}
		dfs(1,0);
		bw.write(ans + "\n");

	}
	
	static void dfs(int n, int p) {
		if(D[n] == 0) return;
		if(D[n] == 1) ans+=2;
		if(D[n] == 2) ans++;
		if(D[n] == 3) ans+=3;
		D[n] = 0;
		for(int i:V[n]) if(i != p) {
			D[i]--;
			dfs(i,n);
		}
	}
	
}

```
