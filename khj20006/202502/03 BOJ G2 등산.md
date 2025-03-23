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
	

	public static void main(String[] args) throws Exception {
		
		int[] dx = {1,0,-1,0};
		int[] dy = {0,1,0,-1};
		
		nextLine();
		int N = nextInt(), M = nextInt(), T = nextInt(), D = nextInt();
		int[][] A = new int[N][M];
		for(int i=0;i<N;i++) {
			String line = br.readLine();
			for(int j=0;j<M;j++) {
				char a = line.charAt(j);
				if(a <= 'Z') A[i][j] = a-'A';
				else A[i][j] = a-'a'+26;
			}
		}
		
		int INF = 1234567890;
		int[][][] dist = new int[N][M][52];
		for(int i=0;i<N;i++) for(int j=0;j<M;j++) Arrays.fill(dist[i][j], INF);
		PriorityQueue<int[]> PQ = new PriorityQueue<>((a,b) -> a[0]-b[0]);
		dist[0][0][A[0][0]] = 0;
		PQ.offer(new int[] {0,0,0,A[0][0]});
		while(!PQ.isEmpty()) {
			int[] now = PQ.poll();
			int t = now[0], x = now[1], y = now[2], a = now[3];
			if(t > dist[x][y][a]) continue;
			for(int i=0;i<4;i++) {
				int xx = x+dx[i], yy = y+dy[i];
				if(xx<0 || xx>=N || yy<0 || yy>=M) continue;
				if(Math.abs(A[x][y] - A[xx][yy]) > T) continue;
				int aa = Math.max(a, A[xx][yy]);
				int v = Math.max(1, A[xx][yy] - A[x][y]);
				if(dist[xx][yy][aa] > t + v*v) {
					dist[xx][yy][aa] = t+v*v;
					PQ.offer(new int[] {t+v*v,xx,yy,aa});
				}
			}
		}
		for(int i=51;i>=0;i--) {
			if(dist[0][0][i] <= D) {
				bw.write(i+"\n");
				bwEnd();
				return;
			}
		}
		
		bwEnd();
	}

}

```
