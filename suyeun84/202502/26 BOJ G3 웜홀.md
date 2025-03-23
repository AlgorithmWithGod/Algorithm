```java
import java.util.*;
import java.io.*;

public class boj1865 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
	static StringTokenizer st;
	
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	static void bwEnd() throws Exception {bw.flush(); bw.close();}
	static ArrayList<Road> road;
	static int N;

	public static void main(String[] args) throws Exception {
		nextLine();
		int TC = nextInt();
		for (int tc = 0; tc < TC; tc++) {
			nextLine();
			N = nextInt(); //지점의 수
			int M = nextInt(); //도로의 갯수
			int W = nextInt(); //웜홀의 갯수
			road = new ArrayList<>(N+1);

			int S, E, T;
			for (int i = 0 ; i < M+W; i++) {
				nextLine();
				S = nextInt();
				E = nextInt();
				T = nextInt();
				if (i < M) {
					road.add(new Road(S, E, T));
					road.add(new Road(E, S, T));
				} else {
					road.add(new Road(S, E, -1*T));
				}
			}
			
			if (bfs()) bw.write("YES"+"\n");
			else bw.write("NO"+"\n");
		}
		bwEnd();
	}
	
	// 음수 사이클 존재하면 true 반환
	static boolean bfs() {
		int[] time = new int[N+1];
		Arrays.fill(time, 10001);
		time[1] = 0;
		
		for (int i = 0; i < N; i++) { //N-1번 반복 + N번째 처리
			for (int j = 0; j < road.size(); j++) { //간선 확인
				Road r = road.get(j);
				if (i == N-1) {
					if (time[r.e] > time[r.s]+r.t) return true;
					continue;
				}
				time[r.e] = Math.min(time[r.e], time[r.s]+r.t);
			}
		}
		return false;
	}

	static class Road {
		int s;
		int e;
		int t;
		public Road(int s, int e, int t) {
			this.s = s;
			this.e = e;
			this.t = t;
		}
	}
}

```
