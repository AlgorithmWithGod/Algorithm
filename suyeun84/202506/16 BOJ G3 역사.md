```java
import java.io.*;
import java.util.*;

public class boj1613 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	
	static int N;
	static int[][] floyd;
	static int INF = 100000000;
	public static void main(String[] args) throws Exception {
		nextLine();
		N = nextInt();
		int K = nextInt();
		floyd = new int[N+1][N+1];
		for (int i = 0; i < N+1; i++) {
			Arrays.fill(floyd[i], INF);
			floyd[i][i] = 0;
		}
		for (int i = 0; i < K; i++) {
			nextLine();
			int a = nextInt();
			int b = nextInt();
			floyd[a][b] = 1;
		}
		solve();
		nextLine();
		int S = nextInt();
		for (int i = 0; i < S; i++) {
			nextLine();
			int a = nextInt();
			int b = nextInt();
			if (floyd[a][b] != INF) System.out.println(-1);
			else if (floyd[b][a] != INF) System.out.println(1);
			else System.out.println(0);
		}
	}
	
	static void solve() {
		for (int k = 1; k <= N; k++) {
			for (int i = 1; i <= N; i++) {
				for (int j = 1; j <= N; j++) {
					if (floyd[i][k] == INF || floyd[k][j] == INF) continue;
					floyd[i][j] = Math.min(floyd[i][j], floyd[i][k]+floyd[k][j]);
				}
			}
		}
	}
}
```
