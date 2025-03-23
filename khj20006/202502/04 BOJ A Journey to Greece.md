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
	static int INF = (int)1e9 + 1;
	static int N, P, M, G, T;
	static int[] p;
	static int[] num;
	static List<int[]>[] V;
	static int[][] dist;
	static int[][] cost;
	static int[][][] dp;
	
	static void sizeInitialize() {
		p = new int[P+1];
		num = new int[N+1];
		V = new ArrayList[N+1];
		for(int i=0;i<=N;i++) V[i] = new ArrayList<>();
		dist = new int[P+1][N+1];
		cost = new int[P+1][P+1];
		dp = new int[P+1][2][1<<(P+1)];
		for(int i=0;i<=P;i++) for(int j=0;j<2;j++) Arrays.fill(dp[i][j], INF);
	}
	
	static void input() throws Exception {
		
		nextLine();
		N = nextInt();
		P = nextInt();
		M = nextInt();
		G = nextInt();
		T = nextInt();
		
		sizeInitialize();
		
		for(int i=1;i<=P;i++) {
			nextLine();
			int a = nextInt(), b = nextInt();
			G -= b;
			p[i] = a;
			num[p[i]] = i;
		}
		
		for(int i=0;i<M;i++) {
			nextLine();
			int a = nextInt(), b = nextInt(), c = nextInt();
			V[a].add(new int[] {b,c});
			V[b].add(new int[] {a,c});
		}
		
	}
	
	static void dijk(int s) {
		Arrays.fill(dist[s], INF);
		
		PriorityQueue<int[]> PQ = new PriorityQueue<>((a,b) -> a[0]-b[0]);
		PQ.offer(new int[] {0,p[s]});
		dist[s][p[s]] = 0;
		while(!PQ.isEmpty()) {
			int[] now = PQ.poll();
			int d = now[0], n = now[1];
			if(d > dist[s][n]) continue;
			for(int[] x : V[n]) {
				int nx = x[0], c = x[1];
				if(dist[s][nx] > d + c) {
					dist[s][nx] = d+c;
					PQ.offer(new int[] {d+c,nx});
				}
			}
		}
		
	}
	
	static void constructNewGraph() {
		for(int i=0;i<=P;i++) for(int j=0;j<=P;j++) cost[i][j] = dist[i][p[j]];
	}
	
	static int solve(int n, int x, int k) {
		if(dp[n][x][k] != INF) return dp[n][x][k];
		int prev = k ^ (1<<n);
		for(int i=0;i<=P;i++) {
			if((prev & (1<<i)) == 0) continue;
			// no taxi
			dp[n][x][k] = Math.min(dp[n][x][k], solve(i,x,prev) + cost[i][n]);
			// can taxi
			if(x == 1) dp[n][x][k] = Math.min(dp[n][x][k], solve(i,0,prev) + T);
		}
		
		return dp[n][x][k];
	}

	public static void main(String[] args) throws Exception {

		input();
		
		for(int i=0;i<=P;i++) dijk(i);
		
		constructNewGraph();
		
		for(int i=1;i<=P;i++) {
			dp[i][0][1<<i] = cost[0][i];
			dp[i][1][1<<i] = T;
		}
		int withoutTaxi = solve(0,0,(1<<(P+1))-1);
		int withTaxi = solve(0,1,(1<<(P+1))-1);
		
		if(withoutTaxi <= G) bw.write("possible without taxi");
		else if(withTaxi <= G) bw.write("possible with taxi");
		else bw.write("impossible");
		
		
		
		bwEnd();
	}

}

```
