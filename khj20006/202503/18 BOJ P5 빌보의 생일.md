```java

import java.util.*;
import java.io.*;

class SegTree{
	int[] tree;
	SegTree(int size){
		tree = new int[size*4+1];
	}
	
	void upt(int s, int e, int i, int n) {
		if(s==e) {
			tree[n] = 1;
			return;
		}
		int m=(s+e)>>1;
		if(i<=m) upt(s,m,i,n*2);
		else upt(m+1,e,i,n*2+1);
		tree[n] = tree[n*2] + tree[n*2+1];
	}
	
	int find(int s, int e, int l, int r, int n) {
		if(l>r || l>e || r<s) return 0;
		if(l<=s && e<=r) return tree[n];
		int m=(s+e)>>1;
		return find(s,m,l,r,n*2) + find(m+1,e,l,r,n*2+1);
	}
}

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
	static SegTree seg;
	static TreeMap<String, Integer> T;
	
	public static void main(String[] args) throws Exception {
		
		for(N = nextInt();N != 0;N = nextInt()) {
			
			ready();
			solve();
		}
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		T = new TreeMap<>();
		seg = new SegTree(N);
		for(int i=1;i<=N;i++) T.put(nextToken(), i);
		
	}
	
	static void solve() throws Exception{
		
		long ans = 0;
		for(int i=1;i<=N;i++) {
			int x = T.get(nextToken());
			ans += seg.find(1, N, x, N, 1);
			seg.upt(1,N,x,1);
		}
		bw.write(ans + "\n");

	}
	
}

```
