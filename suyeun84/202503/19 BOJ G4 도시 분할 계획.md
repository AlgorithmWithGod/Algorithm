```java
import java.io.*;
import java.util.*;

public class boj1647 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	
	static int N, M;
	static ArrayList<Node> roads;
	static int[] parent;
	
	public static void main(String[] args) throws Exception {
		nextLine();
		N = nextInt();
		M = nextInt();
		int a, b, c, answer = 0;
		roads = new ArrayList<>();
		parent = new int[N+1];
		for (int i = 0; i < N+1; i++) parent[i] = i;
		for (int i = 0; i < M; i++) {
			nextLine();
			a = nextInt();
			b = nextInt();
			c = nextInt();
			roads.add(new Node(a,b,c));
		}
		
		roads.sort((o1, o2) -> o1.c-o2.c);
		
		int cnt = 0;
		for (Node road : roads) {
			if (cnt == N-2) break;
			if (find(road.a) != find(road.b)) {
				union(road.a, road.b);
				answer += road.c;
				cnt++;
			}
		}
		System.out.println(answer);
	}
	
	static void union(int a, int b) {
		int A = find(a);
		int B = find(b);
		if (A==B) return;
		if (A<B) parent[B] = A;
		else parent[A] = B;
	}
	
	static int find(int node) {
		if (parent[node] == node) return node;
		return parent[node] = find(parent[node]);
	}
	
	static class Node{
		int a, b, c;
		public Node(int a, int b, int c) {
			this.a = a;
			this.b = b;
			this.c = c;
		}
	}
}

```
