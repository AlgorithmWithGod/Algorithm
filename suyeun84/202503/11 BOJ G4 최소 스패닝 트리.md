```java
import java.util.*;
import java.io.*;

public class boj1197 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
    static int nextInt() {return Integer.parseInt(st.nextToken());}
    
    static ArrayList<Node> graph;
    static int[] parent;
    static int V, E, answer = 0;
  	public static void main(String[] args) throws Exception {
  		nextLine();
  		V = nextInt();
  		E = nextInt();
  		int a, b, c;
  		graph = new ArrayList<>();
  		parent = new int[V+1];
  		for (int i = 1; i < V+1; i++) parent[i] = i;
  		
  		for (int i = 0; i < E; i++) {
  			nextLine();
  			a = nextInt();
  			b = nextInt();
  			c = nextInt();
  			graph.add(new Node(a, b, c));
  		}
  		
  		graph.sort((o1, o2) -> o1.c-o2.c);
  		
  		int edgeCnt = 0;
  		for (int i = 0; i < E; i++) {
  			Node curr = graph.get(i);
  			if (find(curr.s) == find(curr.e)) continue;
  			answer += curr.c;
  			union(curr.s, curr.e);
  			edgeCnt++;
  			if (edgeCnt == V-1) break;
  		}
  		System.out.println(answer);
  	}
  	
  	static void union(int a, int b) {
  		int pa = find(a);
  		int pb = find(b);
  		if (pa != pb) parent[pb] = pa;
  	}
  	
  	static int find(int a) {
  		if (parent[a] == a) return a;
  		else return parent[a] = find(parent[a]);
  	}
	
  	static class Node{
  		int s, e, c;
  		public Node(int s, int e, int c) {
  			this.s = s;
  			this.e = e;
  			this.c = c;
  		}
	  }
}

```
