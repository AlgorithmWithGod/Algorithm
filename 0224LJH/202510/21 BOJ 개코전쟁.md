```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.HashSet;
import java.util.StringTokenizer;

public class Main {
	
	static boolean[] visited;
	static int nodeCnt,edgeCnt,ans;
	static Node[] nodes;
	static int[] cost;
	
	static class Node{
		int num;
		HashSet<Edge> edges = new HashSet<>();
		ArrayList<Node> way = new ArrayList<>(); // 이 곳으로 오기위한 길 기록
		
		public Node(int num) {
			this.num = num;
		}
	}
	
	static class Edge{
		boolean isAlive = true;
		Node from;
		Node to;
		int cost;
		
		public Edge(Node from, Node to, int cost) {
			this.from = from;
			this.to = to;
			this.cost = cost;
		}
	}
	
    public static void main(String[] args) throws IOException {
    	init();
    	process();
    	print();
    }
    
    private static void init() throws IOException{
    	BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    	StringTokenizer st = new StringTokenizer(br.readLine());
    	nodeCnt = Integer.parseInt(st.nextToken());
    	edgeCnt = Integer.parseInt(st.nextToken());
    	ans = 0;
    	
    	visited = new boolean[nodeCnt+1];
    	cost = new int[nodeCnt+1];
    	nodes = new Node[nodeCnt+1];
    	for (int i = 0; i <= nodeCnt; i++) {
    		nodes[i] = new Node(i);
    	}
    	
    	Arrays.fill(cost, Integer.MAX_VALUE);
    	cost[1] = 0;
    	
    	
    	
    	for (int i = 0; i < edgeCnt; i++) {
    		st = new StringTokenizer(br.readLine());
    		Node n1 = nodes[Integer.parseInt(st.nextToken())];
    		Node n2 = nodes[Integer.parseInt(st.nextToken())];
    		int cost = Integer.parseInt(st.nextToken());
    		
    		n1.edges.add(new Edge(n1,n2,cost));
    		n2.edges.add(new Edge(n2,n1,cost));
    	}
    }
    
    private static void process() {
    	HashSet<Node> set =new HashSet<>();
    	for (Node n: nodes) set.add(n);
    	Node node = nodes[1];
    	while (!set.isEmpty()) {
    		set.remove(node);
    		
    		for (Edge e: node.edges) {
    			Node to = e.to;
    			if (cost[to.num] > cost[node.num] + e.cost) {
    				cost[to.num] = cost[node.num] + e.cost;
    				
    				to.way = new ArrayList<>();
    				to.way.addAll(node.way);
    				to.way.add(node);
    			}
    		}
    		
    		int idx = -1;
    		int min = Integer.MAX_VALUE;
    		
    		for (Node n: set) {
//    			System.out.println(cost[n.num]);
    			if (cost[n.num] < min) {
    				min = cost[n.num];
    				idx = n.num;
    			}
    		}
    		if (idx == -1) break;
    		node = nodes[idx];
    		
    		
    	}
    	
    	
    	ArrayList<Node> bestWay = nodes[nodeCnt].way;
    	bestWay.add(nodes[nodeCnt]);
    	int wayLen = bestWay.size();
    	for (int i = 0; i < wayLen-1; i++) {
    		Node cur = bestWay.get(i);
    		Node next = bestWay.get(i+1);
    		
    		for (Edge e: cur.edges) {
    			if (e.to.equals(next)) e.isAlive = false;
    		}
    		for (Edge e: next.edges) {
    			if (e.to.equals(cur)) e.isAlive = false;
    		}
    		
//    		System.out.println(cur.num + "->" + next.num);
    		simulate();
    		
    		for (Edge e: cur.edges) {
    			if (e.to.equals(next)) e.isAlive = true;
    		}
    		for (Edge e: next.edges) {
    			if (e.to.equals(cur)) e.isAlive = true;
    		}
    	}
    	
    }
    
    private static void simulate() {
    	HashSet<Node> set =new HashSet<>();
    	for (Node n: nodes) set.add(n);
    	
    	Arrays.fill(cost, Integer.MAX_VALUE);
    	cost[1] = 0;
    	
    	Node node = nodes[1];
    	while (!set.isEmpty()) {
    		set.remove(node);
    		
    		for (Edge e: node.edges) {
    			if (!e.isAlive) continue;
    			Node to = e.to;
    			if (cost[to.num] > cost[node.num] + e.cost) {
    				cost[to.num] = cost[node.num] + e.cost;
    			}
    		}
    		
    		int idx = -1;
    		int min = Integer.MAX_VALUE;
    		
    		for (Node n: set) {
//    			System.out.println(cost[n.num]);
    			if (cost[n.num] < min) {
    				min = cost[n.num];
    				idx = n.num;
    			}
    		}
    		if (idx == -1) break;
    		node = nodes[idx];
    		
    		
    	}
//    	System.out.println(cost[nodeCnt]);
    	ans = Math.max(ans, cost[nodeCnt]);
    }
    
    private static void print() {
    	System.out.println(ans);
    }

}
```
