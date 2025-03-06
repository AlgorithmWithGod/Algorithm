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
	static int[] r, A;
	static long[] C;
	static boolean[] V;
	static int[][] info;
	
	static int f(int x) {return x==r[x] ? x : (r[x]=f(r[x]));}
	
	public static void main(String[] args) throws Exception {
			
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = Integer.parseInt(br.readLine());
		A = new int[N];
		r = new int[N];
		C = new long[N];
		V = new boolean[N];
		info = new int[N][2];
		nextLine();
		for(int i=0;i<N;i++) {
			A[i] = nextInt();
			r[i] = i;
			C[i] = 1;
			info[i][0] = A[i];
			info[i][1] = i;
		}
		Arrays.sort(info, (a,b) -> b[0]-a[0]);
		
	}
	
	static void solve() throws Exception{
		
		long ans = 0;
		for(int[] n:info) {
			int val = n[0], idx = n[1];
			V[idx] = true;
			if(idx > 0 && V[idx-1]) {
				int x = f(idx-1), y = f(idx);
				C[y] += C[x];
				r[x] = y;
			}
			
			if(idx < N-1 && V[idx+1]) {
				int x = f(idx+1), y = f(idx);
				C[y] += C[x];
				r[x] = y;
			}
			
			ans = Math.max(ans, C[f(idx)] * val);
		}
		bw.write(ans + "\n");
	}
	
}

```
