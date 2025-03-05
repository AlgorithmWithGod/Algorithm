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

	static List<Integer>[] V;
	static int N;
	static int[] A, B;
	static boolean[] vis;
	static int ans = 0, cnt = 0;
	static boolean multiedge;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{

		N = Integer.parseInt(br.readLine());
		A = new int[N];
		B = new int[N];
		
		nextLine();
		for(int i=0;i<N;i++) A[i] = nextInt();
		
		nextLine();
		for(int i=0;i<N;i++) B[i] = nextInt();

		vis = new boolean[1000001];
		V = new List[1000001];
		
		for(int i=0;i<=1000000;i++) V[i] = new ArrayList<>();
		
		for(int i=0;i<N;i++) {
			V[A[i]].add(B[i]);
			V[B[i]].add(A[i]);	
		}
		
		for(int i=0;i<=1000000;i++) if(!V[i].isEmpty()) Collections.sort(V[i]);
		
	}
	
	static void solve() throws Exception{

		for(int i=0;i<=1000000;i++) {
			if(vis[i]) continue;
			multiedge = false;
			cnt = 0;
			vis[i] = true;
			if(dfs(i, -1) && !multiedge) ans += cnt-1;
			else ans += cnt;
		}
		bw.write(ans + "\n");
		
	}
	
	// 트리면 true, 아니면 false
	static boolean dfs(int n, int p) {
		cnt++;
		boolean res = true;
		int prev = -1;
		for(int i=0;i<V[n].size();i++) if(!V[n].get(i).equals(p)) {
			int x = V[n].get(i);
			if(i < V[n].size()-1 && V[n].get(i+1).equals(x)) multiedge = true;
			if(vis[x]) res = false;
			else{
				vis[x] = true;
				res &= dfs(x,n);
			}
		}
		return res;
	}
	
	
}

```
