```java
import java.io.*;
import java.util.*;

public class boj16562 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	
	static int N, M, K, answer;
	static int[] parent, money;
	public static void main(String[] args) throws Exception {
		nextLine();
		N = nextInt();
		M = nextInt();
		K = nextInt();
		parent = new int[N+1];
		money = new int[N+1];
		nextLine();
		for (int i = 1; i < N+1; i++) {
			parent[i] = i;
			money[i] = nextInt();
		}
		for (int i = 0; i < M; i++) {
			nextLine();
			int a = nextInt();
			int b = nextInt();
			union(a, b);
		}
		for (int i = 1; i < N+1; i++) {
			if (find(i) == i) answer += money[i];
		}
		if (K < answer) System.out.println("Oh no");
		else System.out.println(answer);
	}
	static int find(int x) {
		if (x == parent[x]) return x;
		return parent[x] = find(parent[x]);
	}
	
	static void union(int x, int y) {
		x = find(x);
		y = find(y);
		if (money[x] < money[y]) parent[y] = x;
		else parent[x] = y;
	}
}
```
