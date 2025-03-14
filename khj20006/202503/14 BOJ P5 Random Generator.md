```java

import java.util.*;
import java.io.*;

class SegTree{
	int[] tree;
	SegTree(int size){
		tree = new int[size*4+1];
	}
	
	void upt(int s, int e, int i, int v, int n) {
		if(s == e) {
			tree[n] = v;
			return;
		}
		int m=(s+e)>>1;
		if(i <= m) upt(s, m, i, v, n*2);
		else upt(m+1, e, i, v, n*2+1);
		tree[n] = tree[n*2] + tree[n*2+1];
	}
	
	int find(int s, int e, int v, int n) {
		if(s == e) return s;
		int m=(s+e)>>1;
		if(v <= tree[n*2]) return find(s, m, v, n*2);
		return find(m+1, e, v-tree[n*2], n*2+1);
	}
}

class Main {
	
	// IO field
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
	static StringTokenizer st = new StringTokenizer("");

	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() throws Exception {
		if(!st.hasMoreTokens()) nextLine();
		return Integer.parseInt(st.nextToken());
	}
	static long nextLong() throws Exception {
		if(!st.hasMoreTokens()) nextLine();
		return Long.parseLong(st.nextToken());
	}
	static void bwEnd() throws Exception {bw.flush();bw.close();}
	
	// Additional field
	
	static int N;
	static SegTree seg;
	
	public static void main(String[] args) throws Exception {
			
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = nextInt();
		seg = new SegTree(N);
		for(int i=1;i<=N;i++) seg.upt(1, N, i, nextInt(), 1);
		
	}
	
	static void solve() throws Exception{
		
		for(int i=1;i<=N;i++) {
			int p = nextInt();
			int x = seg.find(1, N, p, 1);
			bw.write(x + " ");
			seg.upt(1, N, x, 0, 1);
		}
		
	}
	
}

```
