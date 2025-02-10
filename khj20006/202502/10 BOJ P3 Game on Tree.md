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

	static int[] d;
	static List<Integer>[] V;
	static int N, ans = -1;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
	}
	
	static void ready() throws Exception{
		
		N = Integer.parseInt(br.readLine());
		d = new int[N+1];
		V = new ArrayList[N+1];
		for(int i=1;i<=N;i++) V[i] = new ArrayList<>();
		nextLine();
		for(int i=2;i<=N;i++) {
			int p = nextInt();
			V[p].add(i);
		}
		
	}
	
	static void solve() throws Exception{
		
		dfs(1);
		if(d[1] <= 1) {
			bw.write("FIRST\n");
			bw.write(findAns(1) + "\n");
		}
		else bw.write("SECOND");
		
	}
	
	static void dfs(int n) {
		if(V[n].isEmpty()) d[n] = 2;
		for(int i:V[n]) {
			dfs(i);
			d[n] += Math.max(0, d[i]-1);
		}
	}
	
	static int findAns(int n) {
		if(V[n].isEmpty()) return n;
		int next = n, max = -1;
		for(int i:V[n]) {
			if(d[i] > max) {
				max = d[i];
				next = i;
			}
		}
		return findAns(next);
	}
	
}

```
