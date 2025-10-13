```java

import java.awt.Point;
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
	
	static class Node{
		int idx;
		int x,y;
		public Node(int idx, int x, int y) {
			this.idx = idx;
			this.x = x;
			this.y = y;
		}
	}
	
	static int nodeCnt;
	static Node[] nodes;
	static int[] ans;
	static List<Point> list;

	static StringBuilder sb = new StringBuilder();
    
    public static void main(String[] args) throws NumberFormatException, IOException {
        init();
        process();
        print();

    }
    

    
    public static void init() throws NumberFormatException, IOException {
    	BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    	nodeCnt = Integer.parseInt(br.readLine());
    	nodes = new Node[nodeCnt];
    	ans = new int[nodeCnt];
    	for (int i = 0; i < nodeCnt; i++) {
    		StringTokenizer st = new StringTokenizer(br.readLine());
    		int x = Integer.parseInt(st.nextToken());
    		int y = Integer.parseInt(st.nextToken());
    		nodes[i] = new Node(i, x,y);
    		
    	}
    	
	}
    
    public static void process() throws IOException { 	
    	
    	Arrays.fill(ans, Integer.MAX_VALUE);
    	
    	list = new ArrayList<>(); // 모든 후보 지점 리스트
    	for (int i = 0; i < nodeCnt; i++) {
    		for (int j = 0; j < nodeCnt; j++) {
    			list.add(new Point(nodes[i].x, nodes[j].y));
    		}
    	}
    	calculte();
    	
    	
    	for (int i = 0; i < nodeCnt; i++) {
    		sb.append(ans[i]).append(" ");
    	}
    }
    
    private static void calculte() {
    	for (Point p: list) {
    		int x =p.x;
    		int y = p.y;
    		
    		PriorityQueue<Node> pq = new PriorityQueue<>(
    				(a,b) -> (Math.abs(x - a.x) + Math.abs(y - a.y)) - (Math.abs(x - b.x) + Math.abs(y - b.y)) );
    		for (Node n: nodes) pq.add(n);
    		
    		int distanceSum = 0;
    		for (int i = 0; i < nodeCnt; i++) {
    			Node n = pq.poll();
    			distanceSum += Math.abs(x - n.x) + Math.abs(y - n.y);
    			
    			ans[i] = Math.min(ans[i], distanceSum);
    		}
    	}
    }
   
    



	public static void print() {
		System.out.println(sb.toString());

    }
}
```
