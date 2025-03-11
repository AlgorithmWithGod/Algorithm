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
	
	static long S, F, M;
	static long[] C;
	static boolean[] sieve;
	
	public static void main(String[] args) throws Exception {
			
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		nextLine();
		S = nextLong();
		F = nextLong();
		M = nextLong();
		F += S;
		sieve = new boolean[(int)M+1];
		C = new long[(int)M+1];
		
	}
	
	static void solve() throws Exception{
		
		for(int i=2;i*i<=M;i++) if(!sieve[i]) for(int j=i*i;j<=M;j+=i) sieve[j] = true;
		
		for(int i=2;i<=M;i++) if(!sieve[i]) for(long j=i;j<=F;j*=i) C[i] += F/j;
		for(int i=2;i<=M;i++) if(!sieve[i]) for(long j=i;j<=S;j*=i) C[i] -= S/j;
		for(int i=2;i<=M;i++) if(!sieve[i]) for(long j=i;j<=F-S;j*=i) C[i] -= (F-S)/j;
		
		int ans = 1;
		for(int i=2;i<=M;i++) {
			if(!sieve[i]) {
				if(C[i] > 0) ans = i;
				continue;
			}
			int temp = i, cnt = 0;
			boolean can = true;
			for(int j=2;j*j<=temp;j++) if(!sieve[j] && temp%j == 0) {
				cnt = 0;
				while(temp%j == 0) {
					temp/=j;
					cnt++;
				}
				can &= C[j] >= cnt;
				cnt = 0;
			}
			if(temp != 1) can &= C[temp] >= 1;
			if(can) ans = i;
		}
		bw.write(ans + "\n");
		
	}
	
}

```
