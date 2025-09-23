```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
	
	static int nodeCnt, preCnt,ans;
	static Node[] nodes;;
	static StringBuilder sb = new StringBuilder();
	
	
	static class Node{
		int semester;
		int num;
		int parentCnt;
		HashSet<Node> children;
		
		public Node(int num) {
			semester = 1;
			parentCnt = 0;
			this.num = num;
			children = new HashSet<>();
			
		}
	}

    public static void main(String[] args) throws NumberFormatException, IOException {
    	init();
    	process();
    	print();
    	

    }
    
    public static void init() throws NumberFormatException, IOException {
    	BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    	StringTokenizer st = new StringTokenizer(br.readLine());
    	nodeCnt = Integer.parseInt(st.nextToken());
    	preCnt = Integer.parseInt(st.nextToken());
    	nodes = new Node[nodeCnt+1];
    	for (int i = 1; i <= nodeCnt; i++) {
    		nodes[i] = new Node(i);
    	}
    	
    	for (int i = 0; i < preCnt; i++) {
    		st = new StringTokenizer(br.readLine());
    		int parent = Integer.parseInt(st.nextToken());
    		int child = Integer.parseInt(st.nextToken());
    		
    		nodes[parent].children.add(nodes[child]);
    		nodes[child].parentCnt++;
    		
    	}

    }
    
    public static void process() { 	
    	Queue<Node> pq = new LinkedList<>();
    	
    	for (int i = 1; i <= nodeCnt; i++ ) {
    		
    		Node node = nodes[i];
    		if (node.parentCnt ==0) pq.add(node);
    			
    	}
    	
    	while (!pq.isEmpty()) {
    		Node node = pq.poll();
    		for (Node n: node.children ) {
    			n.parentCnt--;
    			if (n.parentCnt == 0) {
    				n.semester = node.semester+1;
    				pq.add(n);
    			}
    		}
    	}

    	
    	for (int i = 1; i<= nodeCnt; i++) {
    		sb.append(nodes[i].semester+ " ");
    	}
    }



	public static void print() {
		System.out.println(sb.toString());
    }
}
```
