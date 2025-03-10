```java
import java.io.*;
import java.util.*;

public class boj1967 {
	  static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
    static int nextInt() {return Integer.parseInt(st.nextToken());}
    
    static ArrayList<ArrayList<Node>> graph;
    static boolean[] visited;
    static int answer = 0;
	  public static void main(String[] args) throws Exception {
  		nextLine();
  		int n = nextInt();
  		graph = new ArrayList<>(n+1);
  		visited = new boolean[n+1];
  		for (int i = 0; i < n+1; i++) graph.add(new ArrayList<>());
  		for (int i = 0; i < n-1; i++) {
  			nextLine();
  			int a = nextInt();
  			int b = nextInt();
  			int c = nextInt();
  			graph.get(a).add(new Node(b, c));
  			graph.get(b).add(new Node(a, c));
  		}
  		
  		for (int i = 1; i <= n; i++) {
  			if (graph.get(i).size() != 1) continue;
  			visited[i] = true;
  			dfs(i, 0);
  			visited[i] = false;
  		}
  		System.out.println(answer);
    }
	
  	static void dfs(int node, int total) {
  		for (Node n : graph.get(node)) {
  			if (visited[n.n]) continue;
  			visited[n.n] = true;
  			dfs(n.n, total + n.c);
  			visited[n.n] = false;
  		}
  		answer = Math.max(answer, total);
  	}
	
	  static class Node {
  		int n;
  		int c;
  		public Node(int n, int c) {
  			this.n = n;
  			this.c = c;
  		}
	  }
}

```
