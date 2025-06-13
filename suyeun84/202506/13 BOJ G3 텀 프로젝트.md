```java
import java.io.*;
import java.util.*;

public class boj9466 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	
	static int N, cycle;
	static int[] point;
	static boolean[] check, visited;
	public static void main(String[] args) throws Exception {
		nextLine();
		int T = nextInt();
		
		for (int tc = 0; tc < T; tc++) {
			nextLine();
			N = nextInt();
			nextLine();
			point = new int[N+1];
			for (int i = 1; i <= N; i++) point[i] = nextInt();
			cycle = 0;
			check = new boolean[N+1];
			visited = new boolean[N+1];
			
			for (int i = 1; i <= N; i++) {
				if (check[i]) continue;
				dfs(i);
			}
			System.out.println(N - cycle);
		}

	}
	static void dfs(int idx) {
		if (check[idx]) return;
		if (visited[idx]) {
			check[idx] = true;
			cycle++;
		}
		visited[idx] = true;
		dfs(point[idx]);
		check[idx] = true;
		visited[idx] = false;
	}
}
```
