```java
import java.io.*;
import java.util.*;

public class boj17352 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	static StringBuilder sb = new StringBuilder();

	static int N;
	static int[] parents;
	public static void main(String[] args) throws Exception {
		nextLine();
		N = nextInt();
		parents = new int[N+1];
		for (int i = 1; i <= N; i++) parents[i] = i;
		for (int i = 0; i < N-2; i++) {
			nextLine();
			int a = nextInt();
			int b = nextInt();
			union(a, b);
		}
		for (int i = 1; i <= N; i++) {
			if (find(i) == i) sb.append(i).append(' ');
		}
		System.out.println(sb);
	}
	
	static void union(int a, int b) {
		int na = find(a);
		int nb = find(b);
		
		if (na == nb) return;
		parents[nb] = na;
	}
	
	static int find(int a) {
		if (parents[a] == a) return a;
		return parents[a] = find(parents[a]);
	}
}
```
