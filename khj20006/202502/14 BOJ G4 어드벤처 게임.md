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
	static int[] M;
	static char[] T;
	static boolean[][] V;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		//solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = Integer.parseInt(br.readLine());
		while(N != 0) {
			
			M = new int[N+1];
			T = new char[N+1];
			V = new boolean[N+1][N+1];
			
			for(int i=1;i<=N;i++) {
				
				nextLine();
				T[i] = st.nextToken().charAt(0);
				M[i] = nextInt();
				for(int a=nextInt();a!=0;a=nextInt()) V[i][a] = true;
				
			}
			
			solve();
			
			N = Integer.parseInt(br.readLine());
		}
		
	}
	
	static void solve() throws Exception{
		
		if(T[1] == 'T' && M[1] > 0) {
			bw.write("No\n");
			return;
		}
		PriorityQueue<int[]> PQ = new PriorityQueue<>((a,b) -> b[0]-a[0]);
		PQ.offer(new int[] {M[1],1});
		int[] D = new int[N+1];
		Arrays.fill(D, -1);
		D[1] = M[1];
		
		while(!PQ.isEmpty()) {
			int[] now = PQ.poll();
			int money = now[0], n = now[1];
			if(n == N) {
				bw.write("Yes\n");
				return;
			}
			if(money < D[n]) continue;
			for(int i=1;i<=N;i++) {
				if(!V[n][i]) continue;
				if(T[i] == 'T') {
					if(money < M[i]) continue;
					if(D[i] < money-M[i]) {
						D[i] = money-M[i];
						PQ.offer(new int[] {D[i],i});
					}
				}
				else {
					if(D[i] < Math.max(money, M[i])) {
						D[i] = Math.max(money, M[i]);
						PQ.offer(new int[] {D[i],i});
					}
				}
			}
		}
		bw.write("No\n");
		
		
	}
	
}

```
