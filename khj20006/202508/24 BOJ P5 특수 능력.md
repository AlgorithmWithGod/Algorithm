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

	static final int INF = (int)1e9 + 7;

	static int N, M, C;
	static int[][] min, max;

	public static void main(String[] args) throws Exception {

		io = new IOController();

		init();
		solve();

		io.close();

	}

	static void init() throws Exception {

		N = io.nextInt();
		M = io.nextInt();
		C = io.nextInt();
		min = new int[N+1][N+1];
		max = new int[N+1][N+1];
		for(int i=1;i<=N;i++) {
			Arrays.fill(min[i], INF);
			Arrays.fill(max[i], -INF);
		}
		for(int i=0;i<M;i++) {
			int a = io.nextInt();
			int b = io.nextInt();
			int c = io.nextInt();
			min[a][b] = Math.min(min[a][b], c);
			max[a][b] = Math.max(max[a][b], c);
		}

	}

	static void solve() throws Exception {

		int[] dist = new int[N+1];
		Arrays.fill(dist, INF);
		dist[1] = 0;
		PriorityQueue<int[]> pq = new PriorityQueue<>((a,b) -> a[0]-b[0]);
		pq.offer(new int[]{0,1,0});
		while(!pq.isEmpty()) {
			int[] cur = pq.poll();
			int d = cur[0], n = cur[1], t = cur[2];
			if(d > dist[n]) continue;
			for(int i=1;i<=N;i++) if(min[n][i] != INF) {
				if(t<C && dist[i] > d - max[n][i]) {
					dist[i] = d - max[n][i];
					pq.offer(new int[]{dist[i], i, t+1});
				}
				if(dist[i] > d + min[n][i]) {
					dist[i] = d + min[n][i];
					pq.offer(new int[]{dist[i], i, t});
				}
			}
		}
		io.write(dist[N] + "\n");

	}

}
```
