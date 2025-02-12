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
	static boolean[] can;
	static boolean[] on;
	static int N, M;
	static int[] root;
	static int[] cnt;
	static List<Integer>[] V;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
	}
	
	static void ready() throws Exception{

		nextLine();
		N = nextInt();
		M = nextInt();
		d = new int[] {-N,-1,1,N};
		
		can = new boolean[N*N];
		on = new boolean[N*N];
		root = new int[N*N];
		cnt = new int[N*N];
		V = new List[N*N];
		for(int i=0;i<N*N;i++) {
			root[i] = i;
			V[i] = new ArrayList<>();
		}
		
		for(int i=0;i<M;i++) {
			nextLine();
			int a = nextInt(), b = nextInt(), c = nextInt(), d = nextInt();
			int from = coord(a-1,b-1), to = coord(c-1,d-1);
			V[from].add(to);
		}
		
	}
	
	static void solve() throws Exception{

		cnt[0] = 1;
		can[0] = true;
		on[0] = true;
		boolean change;
		
		do {
			
			change = false;

			for(int i=0;i<N*N;i++) {
				if(!can[i]) continue;
				for(int j:V[i]) {
					if(!on[j]) {
						change = true;
						on[j] = true;
						for(int k=0;k<4;k++) {
							int g = j+d[k];
							if(0<=g&&g<N*N && adj(j,g) && on[g]) {
								int x = f(j), y = f(g);
								if(x != y) {
									cnt[y] += cnt[x];
									root[x] = y;
								}
							}
						}
					}
				}
			}
			
			for(int i=1;i<N*N;i++) {
				if(!on[i] || can[i]) continue;
				if(f(0) == f(i)) {
					change = true;
					can[i] = true;
				}
			}
			
		}while(change);

		int ans = 0;
		for(int i=0;i<N*N;i++) if(on[i]) ans++;
		bw.write(ans+"\n");
		
	}
	
	static boolean adj(int x, int y) {
		if(Math.abs(x-y) == 1) {
			if(x/N != y/N) return false;
		}
		return true;
	}
	static int coord(int x, int y) {return x*N+y;}
	static int f(int x) {return x==root[x] ? x : (root[x] = f(root[x]));}
	
}

```
