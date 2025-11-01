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

class SegTree {
	int size;
	long[] tree;
	SegTree(int size) {
		this.size = size;
		tree = new long[size*4];
	}

	void upt(int s, int e, int i, int v, int n) {
		if(s == e) {
			tree[n] += v;
			return;
		}
		int m = (s+e)>>1;
		if(i <= m) upt(s,m,i,v,n*2);
		else upt(m+1,e,i,v,n*2+1);
		tree[n] = tree[n*2] + tree[n*2+1];
	}

	long sum(int s, int e, int l, int r, int n) {
		if(l>r || l>e || r<s) return 0;
		if(l<=s && e<=r) return tree[n];
		int m = (s+e)>>1;
		return sum(s,m,l,r,n*2) + sum(m+1,e,l,r,n*2+1);
	}
}

public class Main {

	static IOController io;

	//

	static int N, Q, root, cnt = 0;
	static SegTree seg;
	static TreeSet<Integer> lower;
	static int[][] events, infos, queries;
	static List<Integer>[] graph, chain;
	static int[] sz, par, dep, cn, ci, ord;
	static long[] ans;

	static void dfs(int n, int p) {
		sz[n] = 1;
		par[n] = p;
		for(int i:graph[n]) {
			dfs(i,n);
			sz[n] += sz[i];
		}
	}

	static void hld(int n, int p, int s, int d) {
		dep[n] = d;
		cn[n] = s;
		ci[n] = chain[s].size();
		chain[s].add(n);
		ord[n] = ++cnt;
		int h = -1;
		for(int i:graph[n]) if(h == -1 || sz[i] > sz[h]) h = i;
		if(h != -1) hld(h,n,s,d);
		for(int i:graph[n]) if(i != h) hld(i,n,i,d+1);
	}

	public static void main(String[] args) throws Exception {

		io = new IOController();

		N = io.nextInt();
		Q = io.nextInt();

		infos = new int[N][];
		for(int i=1;i<=N;i++) infos[i-1] = new int[]{io.nextInt(),i};
		Arrays.sort(infos, (a,b) -> a[0]==b[0] ? a[1]-b[1] : a[0]-b[0]);

		graph = new List[N+1];
		lower = new TreeSet<>();
		for(int i=1;i<=N;i++) lower.add(i);
		for(int i=1;i<=N;i++) graph[i] = new ArrayList<>();
		for(int i=1;i<N;i++) {
			int a = io.nextInt();
			int b = io.nextInt();
			graph[a].add(b);
			lower.remove(b);
		}
		root = lower.higher(0);

		events = new int[2*Q][];
		queries = new int[Q][];
		for(int i=0;i<Q;i++) {
			int a = io.nextInt();
			int b = io.nextInt();
			int l = io.nextInt();
			int r = io.nextInt();
			events[i*2] = new int[]{l, i, -1};
			events[i*2+1] = new int[]{r+1, i, 1};
			queries[i] = new int[]{a,b,l,r};
		}
		Arrays.sort(events, (a,b) -> a[0]==b[0] ? a[1]-b[1] : a[0]-b[0]);

		sz = new int[N+1];
		par = new int[N+1];
		dep = new int[N+1];
		cn = new int[N+1];
		ci = new int[N+1];
		ord = new int[N+1];
		chain = new List[N+1];
		for(int i=1;i<=N;i++) chain[i] = new ArrayList<>();
		dfs(root,0);
		hld(root,0,root,0);

		ans = new long[N];
		seg = new SegTree(N+1);
		int pos = 0;
		for(int[] event : events) {
			int value = event[0], queryIdx = event[1], coef = event[2];
			while(pos < N && infos[pos][0] < value) {
				seg.upt(1,N,ord[infos[pos][1]], infos[pos][0], 1);
				pos++;
			}

			int a = queries[queryIdx][0];
			int b = queries[queryIdx][1];
			while(cn[a] != cn[b]) {
				if(dep[a] > dep[b]) {
					long sum = seg.sum(1,N,ord[cn[a]],ord[a],1);
					ans[queryIdx] += sum * coef;
					a = par[cn[a]];
				}
				else {
					long sum = seg.sum(1,N,ord[cn[b]],ord[b],1);
					ans[queryIdx] += sum * coef;
					b = par[cn[b]];
				}
			}
			if(ci[a] > ci[b]) {
				long sum = seg.sum(1,N,ord[b],ord[a],1);
				ans[queryIdx] += sum * coef;
			}
			else {
				long sum = seg.sum(1,N,ord[a],ord[b],1);
				ans[queryIdx] += sum * coef;
			}
		}

		for(int i=0;i<Q;i++) io.write(ans[i] + "\n");

		io.close();

	}

}
```
