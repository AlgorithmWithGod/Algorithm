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
	static int N, M, K;
	static int[] C, A, L, D, R;
	static List<Integer> G;
	static int turnReverse;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		//solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		int T = Integer.parseInt(br.readLine());
		while(T-- > 0) {
			turnReverse = 0;
			nextLine();
			N = nextInt();
			M = nextInt();
			C = new int[N+1];
			TreeSet<Integer> temp = new TreeSet<>();
			
			nextLine();
			for(int i=0;i<M;i++) {
				int a = nextInt(), origin = a;
				if(a == 1) {
					turnReverse ^= 1;
					continue;
				}
				for(int j=2;j*j<=a;j++) {
					if(a%j != 0) continue;
					while(a%j == 0) a/=j;
					temp.add(j);
				}
				if(a > 75) {
					turnReverse ^= 1;
					continue;
				}
				if(a != 1) temp.add(a);
				C[origin]++;
				
			}
			K = temp.size();
			L = new int[K];
			int idx = 0;
			for(int i:temp) L[idx++] = i;
			
			G = new ArrayList<>();
			for(int i=1;i<=N;i++) {
				int res = 0;
				if(C[i] == 0) continue;
				for(int j=0;j<K;j++) if((i % L[j]) == 0) {
					res |= (1<<j);
				}
				G.add(res);
			}
			
			D = new int[1<<K];
			
			solve();
			
		}
		
	}
	
	static void solve() throws Exception{

		R = new int[G.size()];
		for(int i=0;i<G.size();i++) R[i] = G.get(i);
		
		Arrays.fill(D, -1);
		bw.write(dp(0) == 1 ? "amsminn\n" : "bnb2011\n");
		
	}
	
	static int dp(int n) {
		if(D[n] != -1) return D[n];
		int can = 0;
		for(int r:R) if((n&r) == 0) {
			can++;
			if(dp(n|r) == 0) return D[n] = 1;
		}
		return D[n] = can == 0 ? turnReverse : 0;
	}
	
}

```
