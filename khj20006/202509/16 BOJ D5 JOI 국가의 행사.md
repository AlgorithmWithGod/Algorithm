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

	static final int INF = (int)1e9 + 7;

	static int N, M, K, Q;
	static List<int[]>[] graph;
	static List<Integer>[] tree;
	static List<int[]> edges;
	static int[][] min, par;
	static int[] dep, root, dist;

	public static int f(int x) { return x == root[x] ? x : (root[x] = f(root[x])); }

	public static void main(String[] args) throws Exception {

		io = new IOController();

		N = io.nextInt();
		M = io.nextInt();
		K = io.nextInt();
		Q = io.nextInt();
		graph = new List[N+1];
		tree = new List[N+1];
		root = new int[N+1];
		for(int i=1;i<=N;i++) {
			graph[i] = new ArrayList<>();
			tree[i] = new ArrayList<>();
			root[i] = i;
		}

		edges = new ArrayList<>();
		for(int i=1;i<=M;i++) {
			int a = io.nextInt();
			int b = io.nextInt();
			int c = io.nextInt();
			graph[a].add(new int[]{b,c});
			graph[b].add(new int[]{a,c});
			edges.add(new int[]{a,b,0});
		}

		int[] starts = new int[K];
		for(int i=0;i<K;i++) starts[i] = io.nextInt();
		dijkstra(starts);


		for(int[] edge : edges) edge[2] = Math.min(dist[edge[0]], dist[edge[1]]);
		Collections.sort(edges, (a,b) -> b[2]-a[2]);

		for(int[] edge : edges) {
			int a = edge[0], b = edge[1], c = edge[2];
			int x = f(a), y = f(b);
			if(x == y) continue;
			tree[a].add(b);
			tree[b].add(a);
			root[x] = y;
		}

		par = new int[N+1][17];
		min = new int[N+1][17];
		dep = new int[N+1];
		dfs(1,0,0);

		for(int k=1;k<17;k++) for(int i=1;i<=N;i++) {
			par[i][k] = par[par[i][k-1]][k-1];
			min[i][k] = Math.min(min[i][k-1], min[par[i][k-1]][k-1]);
		}

		while(Q-->0) {
			int a = io.nextInt();
			int b = io.nextInt();
			int ans = Integer.MAX_VALUE;

			int diff = Math.abs(dep[a] - dep[b]);
			for(int k=0;k<17;k++) if((diff & (1<<k)) != 0) {
				if(dep[a] > dep[b]) {
					ans = Math.min(ans, min[a][k]);
					a = par[a][k];
				}
				else {
					ans = Math.min(ans, min[b][k]);
					b = par[b][k];
				}
			}

			for(int k=16;k>=0;k--) if(par[a][k] != par[b][k]) {
				ans = Math.min(ans, Math.min(min[a][k], min[b][k]));
				a = par[a][k];
				b = par[b][k];
			}

			if(a != b) {
				ans = Math.min(ans, Math.min(min[a][0], min[b][0]));
				a = par[a][0];
			}
			ans = Math.min(ans, dist[a]);

			io.write(ans + "\n");
		}

		io.close();

	}

	public static void dijkstra(int[] starts) {
		dist = new int[N+1];
		Arrays.fill(dist, INF);
		PriorityQueue<int[]> pq = new PriorityQueue<>((a,b) -> a[0]-b[0]);
		for(int i=0;i<starts.length;i++) {
			dist[starts[i]] = 0;
			pq.offer(new int[]{0, starts[i]});
		}

		while(!pq.isEmpty()) {
			int[] cur = pq.poll();
			int d = cur[0], n = cur[1];
			if(d > dist[n]) continue;
			for(int[] e:graph[n]) if(dist[e[0]] > d + e[1]) {
				dist[e[0]] = d + e[1];
				pq.offer(new int[]{dist[e[0]], e[0]});
			}
		}
	}

	public static void dfs(int n, int p, int d) {
		dep[n] = d;
		par[n][0] = p;
		min[n][0] = dist[n];
		for(int i:tree[n]) if(i != p) dfs(i, n, d+1);
	}

}
```
