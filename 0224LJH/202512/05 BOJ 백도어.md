```java

import java.util.StringTokenizer;
import java.util.*;
import java.io.*;

public class Main {
   
   static StringBuilder sb = new StringBuilder();
   static HashSet<Integer> set = new HashSet<>();
   static int nodeCnt,edgeCnt;
   static long ans = -1;
   static long[] dis;
   static Node[] nodes;
   static boolean[] canGo,visited;
   
   static class Node implements Comparable<Node>{
	   int num;
	   Map<Integer, Integer> to;
	   
	   public Node (int num) {
		   this.num = num;
		   to = new HashMap<>();
	   }
	   
	   public int compareTo(Node n) {
		   return Long.compare(dis[this.num], dis[n.num]);
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
    	
    	nodes = new Node[nodeCnt];
    	visited = new boolean[nodeCnt];
    	canGo = new boolean[nodeCnt];
    	dis = new long[nodeCnt];
    	Arrays.fill(dis, Long.MAX_VALUE);
    	dis[0] = 0;
    	
    	for (int i = 0; i < nodeCnt; i++) {
    		nodes[i] = new Node(i);
    	}
    	
    	st = new StringTokenizer(br.readLine());
    	for (int i = 0; i < nodeCnt; i++) {
    		canGo[i] = (Integer.parseInt(st.nextToken()) == 1);
    	}
    	
    	for (int i = 0; i < edgeCnt; i++) {
    		st = new StringTokenizer(br.readLine());
    		int from = Integer.parseInt(st.nextToken());
    		int to = Integer.parseInt(st.nextToken());
    		int cost = Integer.parseInt(st.nextToken());
    		
    		nodes[from].to.put(to,cost);
    		nodes[to].to.put(from,cost);
    	}
    	
    }
    
    private static void process() throws IOException {
    	PriorityQueue<Node> pq = new PriorityQueue<>();
    	pq.add(nodes[0]);
    	
    	while(!pq.isEmpty()) {
    		Node n = pq.poll();
    		if (visited[n.num]) continue;
    		visited[n.num] = true;
    		
    		for (int to: n.to.keySet()) {
    			if (to != nodeCnt-1 &&  canGo[to]) {
    				continue;
    			}
    			int cost = n.to.get(to);
    			if (dis[to] > dis[n.num] + cost) {
    				dis[to] = dis[n.num] + cost;
    				pq.add(nodes[to]);
    			}
    		}
    	}
    	
    	if (dis[nodeCnt-1] != Long.MAX_VALUE) ans = dis[nodeCnt-1];
    	
    }
    
   private static void print() {
      System.out.println(ans);
    }

}
```
