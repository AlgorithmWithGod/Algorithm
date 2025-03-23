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
	static boolean[][] know;
	static int[] vis;
	static boolean res = true;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
	}
	
	static void ready() throws Exception{

		N = Integer.parseInt(br.readLine());
		know = new boolean[N+1][N+1];
		vis = new int[N+1];
		nextLine();
		for(int a = nextInt(), b = nextInt();a != -1;) {
			know[a][b] = true;
			know[b][a] = true;
			nextLine();
			a = nextInt();
			b = nextInt();
		}
		
	}
	
	static void solve() throws Exception{
		
		for(int i=1;i<=N;i++) if(vis[i] == 0) {
			vis[i] = 1;
			dfs(i,1);
		}
		if(!res) bw.write("-1");
		else {
			List<Integer> A = new ArrayList<>();
			List<Integer> B = new ArrayList<>();
			for(int i=1;i<=N;i++) if(vis[i] == 1) A.add(i); else B.add(i);
			bw.write("1\n");
			for(int i:A) bw.write(i+" ");
			bw.write("-1\n");
			for(int i:B) bw.write(i+" ");
			bw.write("-1\n");
		}
		
	}
	
	static void dfs(int n, int team) throws Exception {
		if(!res) return;
		List<Integer> next = new ArrayList<>();
		int opposite = team == 1 ? 2 : 1;
		for(int i=1;i<=N;i++) {
			if(know[n][i] || i == n) continue;
			if(vis[i] == 0) {
				vis[i] = opposite;
				next.add(i);
				continue;
			}
			else if(vis[i] == opposite) continue;
			res = false;
			return;
		}
		for(int i:next) {
			dfs(i,opposite);
		}
	}
	
}



```
