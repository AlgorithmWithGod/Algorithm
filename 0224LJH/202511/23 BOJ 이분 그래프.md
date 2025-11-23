```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.HashMap;
import java.util.HashSet;
import java.util.LinkedList;
import java.util.PriorityQueue;
import java.util.Queue;
import java.util.StringTokenizer;

public class Main {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringBuilder sb = new StringBuilder();
	static int nodeCnt, edgeCnt;
	static String ans;
	static Node[] nodes;
	static boolean[] visited;
	
	static class Node{
		int num;
		int team = 0;
		HashSet<Node> set = new HashSet<>();
		public Node(int num) {
			this.num = num;
		}
	}

	
    public static void main(String[] args) throws IOException {
    	int tc = Integer.parseInt(br.readLine());
    	for (int i = 0; i < tc; i++) {
        	init();
        	process();
        	sb.append(ans).append("\n");
    	}
    	print();

    }
    
    private static void init() throws IOException{
    	StringTokenizer st = new StringTokenizer(br.readLine());
    	nodeCnt = Integer.parseInt(st.nextToken());
    	edgeCnt = Integer.parseInt(st.nextToken());
    	
    	nodes = new Node[nodeCnt+1];
    	visited = new boolean[nodeCnt+1];
    	
    	for (int i = 1; i <= nodeCnt; i++) {
    		nodes[i] = new Node(i);
    	}
    	for (int i = 0; i < edgeCnt; i++) {
    		st = new StringTokenizer(br.readLine());
    		Node from = nodes[Integer.parseInt(st.nextToken())];
    		Node to = nodes[Integer.parseInt(st.nextToken())];
    		from.set.add(to);
    		to.set.add(from);
    	}
    	
    }
    
    private static void process() throws IOException {
    	ans = "YES";
    	for (int i = 1; i <= nodeCnt; i++) {
    		Node target = nodes[i];
    		if (visited[target.num]) continue;
    		processRound(target.num);
    		
    		
    	}


    	

    }
    
    private static void processRound(int idx) {
    	nodes[idx].team = idx;
    	Queue<Node> q = new LinkedList<>();
    	q.add(nodes[idx]);
    	while(!q.isEmpty()) {
    		Node n = q.poll();
    		if (visited[n.num]) continue;
    		visited[n.num] = true;
    		
    		int opp = n.team*(-1);
    		
    		for (Node node: n.set) {
    			if(node.team == 0) {
    				node.team = opp;
    				q.add(node);
    			} else if (node.team == opp) {
    				continue;
    			}else {
    				ans = "NO";
    				return;
    			}
    			
    			
    		}
    		
    	}
    	
    }
    
    

	private static void print() {
		System.out.print(sb.toString());
    }

}
```
