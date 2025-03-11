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
	
	static int N;
	static List<Integer>[] V;
	static long[] S;
	static long ans = 0;
	
	public static void main(String[] args) throws Exception {
			
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = Integer.parseInt(br.readLine());
		V = new List[N+1];
		S = new long[N+1];
		for(int i=1;i<=N;i++) V[i] = new ArrayList<>();
		for(int i=1;i<N;i++) {
			nextLine();
			int a = nextInt(), b = nextInt();
			V[a].add(b);
			V[b].add(a);
		}
		
	}
	
	static void solve() throws Exception{
		
		dfs(1,0,0);
		bw.write(ans + "\n");
		
	}
	
	static void dfs(int n, int p, long d) {
		S[n] = 1;
		
		for(int i:V[n]) if(i != p) {
			dfs(i,n,d+1);
			S[n] += S[i];
			ans += S[i] * (N-S[i]);
		}
		
		long temp = 0;
		for(int i:V[n]) if(i != p) {
			
			temp += S[i] * (S[n]-S[i]-1); 
			
		}
		temp = temp/2 + S[n]-1;
		ans += temp * d;
		
	}
	
}

```
