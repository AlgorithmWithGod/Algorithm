```java
import java.io.*;
import java.util.*;

public class boj14621 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	
	static int N, M, answer;
	static char[] gender;
	static Road[] roads;
	static int[] parent;
	public static void main(String[] args) throws Exception {
		nextLine();
		N = nextInt();
		M = nextInt();
		answer = 0;
		nextLine();
		gender = new char[N+1];
		roads = new Road[M];
		parent = new int[N+1];
		for (int i = 1; i <= N; i++) {
			gender[i] = st.nextToken().charAt(0);
			parent[i] = i;
		}
		for (int i = 0; i < M; i++) {
			nextLine();
			int u = nextInt();
			int v = nextInt();
			int d = nextInt();
			roads[i] = new Road(u, v, d);
		}
		Arrays.sort(roads, (o1, o2) -> o1.d-o2.d);
		int cnt = 0;
		for (int i = 0; i < M; i++) {
			if (gender[roads[i].s] == gender[roads[i].e]) continue;
			if (find(roads[i].s) == find(roads[i].e)) continue;
			answer += roads[i].d;
			union(roads[i].s, roads[i].e);
			cnt++;
		}
		if (cnt != N-1) System.out.println(-1);
		else System.out.println(answer);
	}
	
	static int find(int x) {
		if (x == parent[x]) return x;
		return parent[x] = find(parent[x]);
	}
	
	static void union(int x, int y) {
		x = parent[x];
		y = parent[y];
		
		if (x<y) parent[y] = x;
		else parent[x] = y;
	}
	
	static class Road {
		int s, e, d;
		public Road(int s, int e, int d) {
			this.s = s;
			this.e = e;
			this.d = d;
		}
	}
}
```
