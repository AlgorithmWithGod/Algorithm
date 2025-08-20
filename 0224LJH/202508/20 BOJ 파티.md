``` java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;


public class Main {
	static final int MAX = Integer.MAX_VALUE/2;

	static PriorityQueue<Node> nodePq = new PriorityQueue<>();
	static PriorityQueue<Edge> edgePq = new PriorityQueue<>();
	static Node[] nodes;
	static boolean[] visited;
	static int[] dis,totalSum;
	
	static int nodeCnt, edgeCnt, target, ans;
	

	
	static class Node implements Comparable<Node>{
		int num;
		int dis;
		List<Edge> edges;
		
		public Node(int num) {
			this.num = num;
			edges = new ArrayList<>();
		}
		
		public int compareTo(Node n) {
			return this.dis - n.dis;
		}
	}
	
	static class Edge implements Comparable<Edge>{
		int to;
		int weight;
		
		public Edge(int to, int weight) {
			this.to = to;
			this.weight = weight;
		}
		
		@Override
		public int compareTo(Edge e) {
			return this.weight - e.weight;
		}
		
		
	}
	
	public static void main(String[] args) throws IOException {
		init();
		process();
		print();
	}
	
	public static void init() throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		
		nodeCnt = Integer.parseInt(st.nextToken());
		edgeCnt = Integer.parseInt(st.nextToken());
		target = Integer.parseInt(st.nextToken());
		ans = 0;
		
		nodes = new Node[nodeCnt+1];
		totalSum = new int[nodeCnt+1];
		for (int i = 1; i <= nodeCnt; i++) {
			nodes[i] = new Node(i);
		}
		
		for (int i = 0; i < edgeCnt; i++) {
			st = new StringTokenizer(br.readLine());
			int from = Integer.parseInt(st.nextToken());
			int to = Integer.parseInt(st.nextToken());
			int weight = Integer.parseInt(st.nextToken());
			nodes[from].edges.add(new Edge(to,weight));
		}
		
	}
	
	public static void process() {
		for (int i = 1; i <= nodeCnt; i++) {
			makeMinDis(i);
			if (i == target) {
				for (int j = 1; j <= nodeCnt; j++) {
					totalSum[j] += dis[j];
				}
				
			} else {
				totalSum[i] += dis[target];
			}
		}
		
		for (int i = 1; i <= nodeCnt; i++) {
			ans = Math.max(ans,totalSum[i]);
		}
	}
	
	
	private static void makeMinDis(int start) {
		
		dis = new int[nodeCnt+1];
		visited = new boolean[nodeCnt+1];
		Arrays.fill(dis, MAX);
		dis[start] = 0;
		
		nodePq.clear();
		nodePq.add(nodes[start]);
		
		while (!nodePq.isEmpty()) {
			Node n = nodePq.poll();
			int from = n.num;
            
            if (from != start && from == target) break;
			
			if (visited[from]) continue;
			visited[from] = true;
			
			edgePq.clear();
			edgePq.addAll(n.edges);
			
			while (!edgePq.isEmpty()) {
				Edge e = edgePq.poll();
				
				if (visited[e.to]) continue;
				int newDis = dis[from] + e.weight;
				if (newDis < dis[e.to]) {
					dis[e.to] = newDis;
                    nodes[e.to].dis = dis[e.to];
					nodePq.add(nodes[e.to]);
				}
				
			}
		}
		
	}

	public static void print() {
		System.out.println(ans);
	}
}
```
