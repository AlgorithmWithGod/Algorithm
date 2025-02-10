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
	static int[] P, in, out, ord;
	static List<Integer>[] V;
	static int N, num = 0;
	static List<Integer>[] seg;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
	}
	
	static void ready() throws Exception{

		N = Integer.parseInt(br.readLine());
		P = new int[N+1];
		V = new List[N+1];
		in = new int[N+1];
		out = new int[N+1];
		ord = new int[N+1];
		seg = new List[4*N+1];
		for(int i=1;i<=N;i++) V[i] = new ArrayList<>();
		
		for(int i=1;i<=N;i++) P[i] = Integer.parseInt(br.readLine());
		for(int i=2;i<=N;i++) V[Integer.parseInt(br.readLine())].add(i);
		
	}
	
	static void solve() throws Exception{

		dfs(1);
		init(1,N,1);
		for(int i=1;i<=N;i++) {
			int res = find(1,N,in[i]+1,out[i],P[i],1);
			bw.write(res+"\n");
		}
		
	}

	static void dfs(int n) {
		in[n] = ++num;
		ord[num] = n;
		for(int i:V[n]) dfs(i);
		out[n] = num;
	}
	
	static void init(int s, int e, int n) {
		if(s==e) {
			seg[n] = new ArrayList<>();
			seg[n].add(P[ord[s]]);
			return;
		}
		int m=(s+e)>>1;
		init(s,m,n*2); init(m+1,e,n*2+1);
		seg[n] = merge(seg[n*2], seg[n*2+1]);
	}
	
	static List<Integer> merge(List<Integer> A, List<Integer> B){
		List<Integer> result = new ArrayList<>();
		int l = 0, r = 0;
		while(l<A.size() && r<B.size()) {
			if(A.get(l) < B.get(r)) {
				result.add(A.get(l));
				l++;
			}
			else {
				result.add(B.get(r));
				r++;
			}
		}
		while(l<A.size()) result.add(A.get(l++));
		while(r<B.size()) result.add(B.get(r++));
		return result;
	}
	
	static int find(int s, int e, int l, int r, int v, int n) {
		if(l>r || l>e || r<s) return 0;
		if(l<=s && e<=r) return seg[n].size() - upperBound(seg[n],v);
		int m=(s+e)>>1;
		return find(s,m,l,r,v,n*2) + find(m+1,e,l,r,v,n*2+1);
	}
	
	static int upperBound(List<Integer> A, int k) {
		int s = 0, e = A.size() - 1, m = (s+e)>>1;
		if(k >= A.get(A.size()-1)) return A.size();
		if(k < A.get(0)) return 0;
		while(s < e) {
			if(A.get(m) <= k) s = m+1;
			else e = m;
			m = (s+e)>>1;
		}
		return m;
	}
	
}

```
