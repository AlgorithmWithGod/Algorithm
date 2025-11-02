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

	static int N, R, Q;
	static int[][] edges;
	static List<int[]>[] graph;
	static int[] root, dep;
	static int[][] par, max;
	static TreeMap<Integer, TreeMap<Integer, Integer>> help;

	public static int f(int x) { return x == root[x] ? x : (root[x] = f(root[x])); }

	public static void dfs(int n, int p, int d) {
		par[n][0] = p;
		dep[n] = d;
		for(int[] e:graph[n]) if(e[0] != p) {
			dfs(e[0], n, d+1);
			max[e[0]][0] = e[1];
		}
	}

	public static void main(String[] args) throws Exception {

		io = new IOController();

		N = io.nextInt();
		R = io.nextInt();
		edges = new int[R][];
		for(int i=0;i<R;i++) edges[i] = new int[]{io.nextInt(),io.nextInt(),io.nextInt()};
		Arrays.sort(edges, (a,b) -> a[2]-b[2]);

		graph = new List[N+1];
		root = new int[N+1];
		for(int i=1;i<=N;i++) {
			graph[i] = new ArrayList<>();
			root[i] = i;
		}

		help = new TreeMap<>();
		int mst = 0;
		for(int[] edge : edges) {
			int a = edge[0], b = edge[1], c = edge[2];
			if(!help.containsKey(a)) help.put(a, new TreeMap<>());
			help.get(a).put(b, c);
			if(!help.containsKey(b)) help.put(b, new TreeMap<>());
			help.get(b).put(a, c);
			int x = f(a), y = f(b);
			if(x == y) continue;
			mst += c;
			root[x] = y;
			graph[a].add(new int[]{b,c});
			graph[b].add(new int[]{a,c});
		}

		par = new int[N+1][17];
		dep = new int[N+1];
		max = new int[N+1][17];
		dfs(1,0,0);
		for(int k=1;k<17;k++) for(int i=1;i<=N;i++) {
			par[i][k] = par[par[i][k-1]][k-1];
			max[i][k] = Math.max(max[i][k-1], max[par[i][k-1]][k-1]);
		}

		for(Q = io.nextInt(); Q-->0;) {
			int a = io.nextInt(), b = io.nextInt();
			int c = help.get(a).get(b);

			int rem = 0;
			int diff = Math.abs(dep[a] - dep[b]);
			for(int k=0;k<17;k++) if((diff & (1<<k)) != 0) {
				if(dep[a] > dep[b]) {
					rem = Math.max(rem, max[a][k]);
					a = par[a][k];
				}
				else {
					rem = Math.max(rem, max[b][k]);
					b = par[b][k];
				}
			}

			for(int k=16;k>=0;k--) if(par[a][k] != par[b][k]) {
				rem = Math.max(rem, Math.max(max[a][k], max[b][k]));
				a = par[a][k];
				b = par[b][k];
			}

			if(a != b) {
				rem = Math.max(rem, Math.max(max[a][0], max[b][0]));
			}

			io.write((mst + c - rem) + "\n");
		}

		io.close();

	}

}
```
