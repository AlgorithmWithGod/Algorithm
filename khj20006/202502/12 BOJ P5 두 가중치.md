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
	static int[][] D;
	static int[][] cost1;
	static int[][] cost2;
	
	static int N;
	static final int INF = (int)1e9 + 5;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
	}
	
	static void ready() throws Exception{

		N = Integer.parseInt(br.readLine());
		D = new int[N][N*9+1];
		for(int i=0;i<N;i++) Arrays.fill(D[i], INF);
		
		cost1 = new int[N][N];
		for(int i=0;i<N;i++) {
			char[] arr = br.readLine().toCharArray();
			for(int j=0;j<N;j++) {
				if(arr[j] == '.') continue;
				cost1[i][j] = arr[j]-'0';
			}
		}
		
		cost2 = new int[N][N];
		for(int i=0;i<N;i++) {
			char[] arr = br.readLine().toCharArray();
			for(int j=0;j<N;j++) {
				if(arr[j] == '.') continue;
				cost2[i][j] = arr[j]-'0';
			}
		}
		
	}
	
	static void solve() throws Exception{

		PriorityQueue<int[]> PQ = new PriorityQueue<>((a,b) -> a[0]-b[0]);
		PQ.offer(new int[] {0,0,0});
		D[0][0] = 0;
		while(!PQ.isEmpty()) {
			int[] now = PQ.poll();
			int w = now[0], s = now[1], n = now[2];
			if(w > D[n][s]) continue;
			for(int i=0;i<N;i++) {
				if(cost1[n][i] == 0) continue;
				if(s+cost1[n][i] <= N*9 && D[i][s+cost1[n][i]] > w + cost2[n][i]) {
					D[i][s+cost1[n][i]] = w + cost2[n][i];
					PQ.offer(new int[] {w+cost2[n][i],s+cost1[n][i],i});
				}
			}
		}
		
		int ans = INF;
		for(int i=0;i<=N*9;i++) if(D[1][i] != INF) ans = Math.min(ans, D[1][i]*i);
		bw.write((ans==INF ? -1 : ans) + "\n");
		
	}
	
	
}

```
