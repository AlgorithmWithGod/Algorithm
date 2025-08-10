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

	static class Node {
		int idx, val;
		Node(int idx, int val) {
			this.idx = idx;
			this.val = val;
		}

		@Override
		public boolean equals(Object o) {
			if (o == null || getClass() != o.getClass())
				return false;
			Node node = (Node)o;
			return idx == node.idx && val == node.val;
		}

		@Override
		public int hashCode() {
			return Objects.hash(idx, val);
		}
	}

	static final long INF = (long)1e18 + 7;

	static int N, K;
	static int[][] x, y;
	static int[] xpos, ypos;
	static List<Node>[] z;
	static int[] rz;
	static PriorityQueue<long[]> pq;
	static long[] dist;

	public static void main(String[] args) throws Exception {

		io = new IOController();

		init();
		solve();

		io.close();

	}

	static void init() throws Exception {

		N = io.nextInt();
		K = io.nextInt();
		x = new int[N][];
		y = new int[N][];
		z = new List[K];
		rz = new int[N];
		for(int i=0;i<K;i++) z[i] = new ArrayList<>();
		for(int i=0;i<N;i++) {
			int X = io.nextInt();
			int Y = io.nextInt();
			int Z = io.nextInt();
			rz[i] = Z;
			x[i] = new int[]{i,X};
			y[i] = new int[]{i,Y};
			z[Z%K].add(new Node(i,Z));
		}

	}

	static void solve() throws Exception {

		Arrays.sort(x, (a,b) -> a[1]==b[1] ? a[0]-b[0] : a[1]-b[1]);
		Arrays.sort(y, (a,b) -> a[1]==b[1] ? a[0]-b[0] : a[1]-b[1]);
		for(int i=0;i<K;i++) Collections.sort(z[i], (a,b) -> a.val==b.val ? a.idx-b.idx : a.val-b.val);

		xpos = new int[N];
		for(int i=0;i<N;i++) xpos[x[i][0]] = i;
		ypos = new int[N];
		for(int i=0;i<N;i++) ypos[y[i][0]] = i;

		dist = new long[N];
		Arrays.fill(dist, INF);
		dist[0] = 0;
		pq = new PriorityQueue<>((a,b) -> Long.compare(a[0],b[0]));
		pq.offer(new long[]{0,0});
		while(!pq.isEmpty()) {
			long[] cur = pq.poll();
			int n = (int)cur[1];
			long d = cur[0];
			if(d > dist[n]) continue;
			z[rz[n]%K].remove(new Node(n, rz[n]));
			int X = xpos[n];
			if(X>0) process(x[X-1][0], d + x[X][1]-x[X-1][1]);
			if(X<N-1) process(x[X+1][0], d + x[X+1][1]-x[X][1]);
			int Y = ypos[n];
			if(Y>0) process(y[Y-1][0], d + y[Y][1]-y[Y-1][1]);
			if(Y<N-1) process(y[Y+1][0], d + y[Y+1][1]-y[Y][1]);
			int RZ = rz[n]%K;
			int NZ = (K-RZ)%K;
			for(Node next:z[NZ]) if(next.idx != n) {
				process(next.idx, d + rz[n] + next.val);
			}
		}
		for(int i=0;i<N;i++) io.write(dist[i] + "\n");

	}

	static void process(int next, long d) {
		if(dist[next] > d) {
			dist[next] = d;
			pq.offer(new long[]{dist[next], next});
		}
	}



}
```
