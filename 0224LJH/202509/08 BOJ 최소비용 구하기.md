```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
	static int cityCnt, busCnt,start,goal;
	static int[] distance;
	static boolean[] visited;
	static Node[] nodes;
	static PriorityQueue<Node> pq = new PriorityQueue<>();
	
	static class Node implements Comparable<Node>{
		int num;
		Map<Integer, Integer> costs = new HashMap<>();
		
		public Node(int num) {
			this.num = num;
		}
		
		@Override
		public int compareTo(Node o) {
			return Integer.compare(distance[this.num], distance[o.num]);
		}
	}

    
    public static void main(String[] args) throws NumberFormatException, IOException {
		init();
		process();
		print();
    }
    
    public static void init() throws NumberFormatException, IOException {
    	BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    	cityCnt = Integer.parseInt(br.readLine());
    	busCnt = Integer.parseInt(br.readLine());
    	nodes = new Node[cityCnt+1];
    	distance = new int[cityCnt+1];
    	visited = new boolean[cityCnt+1];
    	for (int i = 0; i <= cityCnt; i++) {
    		nodes[i] = new Node(i);
    	}
    	
    	for (int i = 0; i < busCnt; i++) {
    		StringTokenizer st = new StringTokenizer (br.readLine());
    		int from = Integer.parseInt(st.nextToken());
    		int to = Integer.parseInt(st.nextToken());
    		int cost = Integer.parseInt(st.nextToken());
    		
    		if (nodes[from].costs.containsKey(to)) {
    			int smaller = Math.min(cost, nodes[from].costs.get(to));
    			nodes[from].costs.replace(to, smaller);
    		} else {
    			nodes[from].costs.put(to, cost);
    		}
    		
    	}
    	
    	StringTokenizer st = new StringTokenizer(br.readLine());
    	start = Integer.parseInt(st.nextToken());
    	goal = Integer.parseInt(st.nextToken());
    	
    	Arrays.fill(distance, Integer.MAX_VALUE/2);
    	distance[start] = 0;
    }
    
    public static void process() {
    	pq.add(nodes[start]);
    	
    	while(!pq.isEmpty()) {
    		Node n = pq.poll();
    		if (visited[n.num]) continue;
    		visited[n.num] = true;
    		
    		for (int to: n.costs.keySet()) {
    			if(visited[to]) continue;
    			int cost = n.costs.get(to);
    			int nDistance = distance[n.num] + cost;
    			if (distance[to] > nDistance) {
    				distance[to] = nDistance;
    				pq.add(nodes[to]);
    			}
    		}
    		
    	}

    }

    public static void print() {
    	System.out.println(distance[goal]);
    }
}
```
