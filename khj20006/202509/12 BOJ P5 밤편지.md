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

	static final int INF = 715827881;

	static int N, M;
	static int[][] cost, dist, val, queries;

	public static void main(String[] args) throws Exception {

		io = new IOController();

		N = io.nextInt();
		M = io.nextInt();
		cost = new int[N+1][N+1];
		dist = new int[N+1][N+1];
		val = new int[N+1][N+1];
		for(int i=1;i<=N;i++) for(int j=1;j<=N;j++) {
			cost[i][j] = io.nextInt();
			if(cost[i][j] == 0 && i != j) cost[i][j] = INF;
			if(i != j) {
				dist[i][j] = INF;
				val[i][j] = INF;
			}
		}

		queries = new int[M][];
		for(int i=0;i<M;i++) queries[i] = new int[]{io.nextInt(),io.nextInt(),io.nextInt(),i};
		Arrays.sort(queries, (a,b) -> a[0]-b[0]);

		int limit = 1;
		int[] ans = new int[M];
		for(int[] query : queries) {
			int c = query[0], s = query[1], e = query[2], i = query[3];
			while(limit < c) {
				for(int x=limit;x<=N;x++) for(int y=x;y<=N;y++) for(int k=1;k<limit;k++) {
					val[x][y] = Math.min(val[x][y], cost[x][limit] + dist[limit][k] + cost[k][y]);
					val[x][y] = Math.min(val[x][y], cost[x][k] + dist[k][limit] + cost[limit][y]);
				}
				for(int k=1;k<=limit;k++) {
					dist[limit][k] = Math.min(dist[limit][k], cost[limit][k]);
					dist[k][limit] = Math.min(dist[k][limit], cost[k][limit]);
				}
				for(int j=1;j<=limit;j++) for(int k=1;k<=limit;k++) dist[j][k] = Math.min(dist[j][k], dist[j][limit] + dist[limit][k]);
				limit++;
			}
			if(s == e) ans[i] = 0;
			else {
				if(s > e) {
					int t = s;
					s = e;
					e = t;
				}
				if(s < c && e < c) ans[i] = dist[s][e] == INF ? -1 : dist[s][e];
				else if(s < c) {
					int res = INF;
					for(int k=1;k<c;k++) res = Math.min(res, dist[s][k] + cost[k][e]);
					ans[i] = res == INF ? -1 : res;
				}
				else {
					if(val[s][e] == INF) ans[i] = cost[s][e] == INF ? -1 : cost[s][e];
					else ans[i] = val[s][e] == INF ? -1 : val[s][e];
				}
			}
		}

		for(int i=0;i<M;i++) io.write(ans[i] + "\n");

		io.close();

	}

}
```
