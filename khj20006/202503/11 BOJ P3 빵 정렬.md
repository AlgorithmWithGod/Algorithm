```java

import java.util.*;
import java.io.*;

class SegTree{
	int[] tree;
	SegTree(int size){
		tree = new int[size*4 + 1];
	}
	void upt(int s, int e, int i, int n) {
		if(s == e) {
			tree[n]++;
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
	static StringTokenizer st;

	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	static long nextLong() {return Long.parseLong(st.nextToken());}
	static void bwEnd() throws Exception {bw.flush();bw.close();}
	
	// Additional field
	
	static int N;
	static int[] A, pos;
	static boolean[] vis;
	static SegTree seg;
	
	public static void main(String[] args) throws Exception {
			
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = Integer.parseInt(br.readLine());
		A = new int[N+1];
		pos = new int[N+1];
		vis = new boolean[N+1];
		seg = new SegTree(N);
		
		nextLine();
		for(int i=1;i<=N;i++) {
			int a = nextInt();
			A[i] = a;
			pos[a] = i;
		}
		
	}
	
	static void solve() throws Exception{
		
		int s = 1, e = 2;
		nextLine();
		for(int i=1;i<=N-2;i++) {
			int b = nextInt();
			int p = pos[b] - seg.find(1, N, 1, pos[b], 1);
			vis[b] = true;
			while(vis[A[s]]) s++;
			while(vis[A[e]] || s >= e) e++;
			seg.upt(1, N, pos[b], 1);
			if(p%2 != 0) continue;
			int temp = pos[A[s]];
			pos[A[s]] = pos[A[e]];
			pos[A[e]] = temp;
			temp = A[s];
			A[s] = A[e];
			A[e] = temp;
		}
		
		int p = nextInt(), q = nextInt();
		if(p == A[s] && q == A[e]) bw.write("Possible");
		else bw.write("Impossible");
		
	}
	
}

```
