# C++
```cpp
#include <bits/stdc++.h>
using namespace std;

int N, Q;
vector<vector<pair<int, int>>> v(300001);
int par[300001][19]{}, mx[300001][19]{}, dep[300001]{};
int lca[1048576]{}, dist[1048576]{};

void dfs(int n, int p, int d) {
	par[n][0] = p, dep[n] = d;
	for(auto [i,c]:v[n]) if(i != p) {
		mx[i][0] = c;
		dfs(i,n,d+1);
	}
}

pair<int,int> mrg(pair<int,int> A, pair<int,int> B) {
	if(A.first == -1) return B;
	if(B.first == -1) return A;
	int a = A.first, b = B.first, res = max(A.second, B.second);
	int diff = abs(dep[a]-dep[b]);
	for(int k=0;k<19;k++) if(diff & (1<<k)) {
		if(dep[a] > dep[b]) res = max(res, mx[a][k]), a = par[a][k];
		else res = max(res, mx[b][k]), b = par[b][k];
	}
	for(int k=18;k>=0;k--) if(par[a][k] != par[b][k]) {
		res = max({res, mx[a][k], mx[b][k]});
		a = par[a][k], b = par[b][k];
	}
	if(a != b) res = max({res, mx[a][0], mx[b][0]}), a = par[a][0];
	return {a, res};
}

void init(int s, int e, int n) {
	if(s == e) {
		lca[n] = s;
		return;
	}
	int m = (s+e)>>1;
	init(s,m,n*2);	init(m+1,e,n*2+1);
	auto [a, b] = mrg({lca[n*2], dist[n*2]}, {lca[n*2+1], dist[n*2+1]});
	lca[n] = a, dist[n] = b;
}

pair<int,int> find(int s, int e, int l, int r, int n) {
	if(l>r || l>e || r<s) return {-1,0};
	if(l<=s && e<=r) return {lca[n], dist[n]};
	int m = (s+e)>>1;
	auto a = find(s,m,l,r,n*2);
	auto b = find(m+1,e,l,r,n*2+1);
	return mrg(a,b);
}

int main(){
	cin.tie(0)->sync_with_stdio(0);

	cin>>N>>Q;
	for(int i=1,a,b,c;i<N;i++) {
		cin>>a>>b>>c;
		v[a].emplace_back(b,c);
		v[b].emplace_back(a,c);
	}

	dfs(1,0,0);
	for(int k=1;k<19;k++) for(int i=1;i<=N;i++) {
		par[i][k] = par[par[i][k-1]][k-1];
		mx[i][k] = max(mx[i][k-1], mx[par[i][k-1]][k-1]);
	}
	init(1,N,1);
	for(int a,b;Q--;cout<<find(1,N,a,b,1).second<<'\n') cin>>a>>b;

}
```

# Java
```java
import java.util.*;
import java.io.*;

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
		while (!st.hasMoreTokens()) nextLine();
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
	static List<int[]>[] graph;
	static int[][] par, max;
	static int[] dep;

	static int[][] seg;

	public static void main(String[] args) throws Exception {

		io = new IOController();

		init();
		solve();

		io.close();

	}

	static void init() throws Exception {

		N = io.nextInt();
		Q = io.nextInt();
		graph = new List[N+1];
		for(int i=1;i<=N;i++) graph[i] = new ArrayList<>();
		for(int i=1;i<N;i++) {
			int a = io.nextInt();
			int b = io.nextInt();
			int c = io.nextInt();
			graph[a].add(new int[]{b,c});
			graph[b].add(new int[]{a,c});
		}
		par = new int[N+1][19];
		max = new int[N+1][19];
		dep = new int[N+1];
		seg = new int[4*N][2];

	}

	static void solve() throws Exception {

		dfs(1,0,0);
		for(int k=1;k<19;k++) for(int i=1;i<=N;i++) {
			par[i][k] = par[par[i][k-1]][k-1];
			max[i][k] = Math.max(max[i][k-1], max[par[i][k-1]][k-1]);
		}

		initSeg(1,N,1);

		for(int a, b;Q-->0;) {
			a = io.nextInt();
			b = io.nextInt();
			io.write(find(1,N,a,b,1)[1] + "\n");
		}

	}

	static void dfs(int n, int p, int d) {
		par[n][0] = p;
		dep[n] = d;
		for(int[] e:graph[n]) if(e[0] != p) {
			max[e[0]][0] = e[1];
			dfs(e[0],n,d+1);
		}
	}

	static int[] lca(int[] A, int[] B) {
		if(A[0] == -1) return B;
		if(B[0] == -1) return A;

		int a = A[0], b = B[0];
		int res = Math.max(A[1], B[1]);

		int diff = Math.abs(dep[a]-dep[b]);
		for(int k=0;k<19;k++) if((diff & (1<<k)) != 0) {
			if(dep[a] > dep[b]) {
				res = Math.max(res, max[a][k]);
				a = par[a][k];
			}
			else {
				res = Math.max(res, max[b][k]);
				b = par[b][k];
			}
		}
		for(int k=18;k>=0;k--) if(par[a][k] != par[b][k]) {
			res = Math.max(res, Math.max(max[a][k], max[b][k]));
			a = par[a][k];
			b = par[b][k];
		}
		if(a != b) {
			res = Math.max(res, Math.max(max[a][0], max[b][0]));
			a = par[a][0];
		}
		return new int[]{a, res};
	}

	static void initSeg(int s, int e, int n) {
		if(s == e) {
			seg[n][0] = s;
			return;
		}
		int m = (s+e)>>1;
		initSeg(s,m,n*2);
		initSeg(m+1,e,n*2+1);
		seg[n] = lca(seg[n*2], seg[n*2+1]);
	}

	static int[] find(int s, int e, int l, int r, int n) {
		if(l>r || l>e || r<s) return new int[]{-1,0};
		if(l<=s && e<=r) return seg[n];
		int m = (s+e)>>1;
		return lca(find(s,m,l,r,n*2), find(m+1,e,l,r,n*2+1));
	}

}
```
