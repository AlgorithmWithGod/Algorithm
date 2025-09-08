```java
import java.io.*;
import java.util.*;

class IOController {
	BufferedReader br;
	BufferedWriter bw;
	StringTokenizer st;

	public IOController() {
		br = new BufferedReader(new InputStreamReader(System.in));
		bw = new BufferedWriter(new OutputStreamWriter(System.out));
		st = new StringTokenizer("");
	}

	String nextLine() throws Exception {
		String line = br.readLine();
		st = new StringTokenizer(line);
		return line;
	}

	String nextToken() throws Exception {
		while (!st.hasMoreTokens())
			nextLine();
		return st.nextToken();
	}

	int nextInt() throws Exception {
		return Integer.parseInt(nextToken());
	}

	long nextLong() throws Exception {
		return Long.parseLong(nextToken());
	}

	double nextDouble() throws Exception {
		return Double.parseDouble(nextToken());
	}

	void close() throws Exception {
		bw.flush();
		bw.close();
	}

	void write(String content) throws Exception {
		bw.write(content);
	}

}

public class Main {

	static IOController io;

	//

	static int N, Q;
	static int[][] seg, lazy;
	static int[] in, out, rev, d, par;
	static List<int[]>[] graph;
	static int order = 0;

	public static void main(String[] args) throws Exception {

		io = new IOController();

		N = io.nextInt();
		graph = new List[N+1];
		in = new int[N+1];
		out = new int[N+1];
		rev = new int[N+1];
		d = new int[N+1];
		par = new int[N+1];
		seg = new int[4*N][20];
		lazy = new int[4*N][20];
		for(int i=1;i<=N;i++) graph[i] = new ArrayList<>();
		for(int i=1;i<N;i++) {
			int a = io.nextInt();
			int b = io.nextInt();
			int c = io.nextInt();
			graph[a].add(new int[]{b,c});
			graph[b].add(new int[]{a,c});
		}

		dfs(1,0,0);

		for(int i=0;i<20;i++) init(1,N,1,i);

		for(Q=io.nextInt();Q-->0;) {
			int o = io.nextInt();
			int x = io.nextInt();
			int y = io.nextInt();
			if(o == 1) {
				int g = par[x] ^ y;
				for(int k=0;k<20;k++) if((g & (1<<k)) != 0) update(1,N,in[x],out[x],1,k);
				par[x] = y;
			}
			else {
				long ans = 0;
				for(int k=0;k<20;k++) {
					long o1 = find(1,N,in[x],out[x],1,k), z1 = (out[x]-in[x]+1) - o1;
					long o2 = find(1,N,in[y],out[y],1,k), z2 = (out[y]-in[y]+1) - o2;
					ans += (o1*z2 + o2*z1) * (1L<<k);
				}
				io.write(ans + "\n");
			}
		}

		io.close();

	}

	static void dfs(int n, int p, int v) {
		d[n] = v;
		in[n] = ++order;
		rev[order] = n;
		for(int[] e:graph[n]) if(e[0] != p) {
			dfs(e[0],n,v^e[1]);
			par[e[0]] = e[1];
		}
		out[n] = order;
	}

	static void init(int s, int e, int n, int x) {
		if(s == e) {
			seg[n][x] = (d[rev[s]] & (1<<x)) == 0 ? 0 : 1;
			return;
		}
		int m = (s+e)>>1;
		init(s,m,n*2,x);
		init(m+1,e,n*2+1,x);
		seg[n][x] = seg[n*2][x] + seg[n*2+1][x];
	}

	static void prop(int s, int e, int n, int x) {
		if(lazy[n][x] != 0) {
			seg[n][x] = e-s+1 - seg[n][x];
			if(s != e) {
				lazy[n*2][x] ^= 1;
				lazy[n*2+1][x] ^= 1;
			}
			lazy[n][x] = 0;
		}
	}

	static void update(int s, int e, int l, int r, int n, int x) {
        prop(s,e,n,x);
		if(l>r || l>e || r<s) return;
		if(l<=s && e<=r) {
			seg[n][x] = e-s+1 - seg[n][x];
			if(s != e) {
				lazy[n*2][x] ^= 1;
				lazy[n*2+1][x] ^= 1;
			}
			return;
		}
		int m = (s+e)>>1;
		update(s,m,l,r,n*2,x);
		update(m+1,e,l,r,n*2+1,x);
        seg[n][x] = seg[n*2][x] + seg[n*2+1][x];
	}

	static int find(int s, int e, int l, int r, int n, int x) {
        prop(s,e,n,x);
		if(l>r || l>e || r<s) return 0;
		if(l<=s && e<=r) return seg[n][x];
		int m = (s+e)>>1;
		return find(s,m,l,r,n*2,x) + find(m+1,e,l,r,n*2+1,x);
	}

}
```
