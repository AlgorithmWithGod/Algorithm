```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

class Main {
	
	static int nodeCnt,ans;
	static Node[] nodes;
	
	static class Node{
		int startTime = 0;
		int cost;
		int parentLeft;
		
		HashSet<Node> children = new HashSet<>();
		
		public Node() {

		}
		
	}
    
    public static void main(String[] args) throws NumberFormatException, IOException {
       init();
       process();
       print();

    }

    
    public static void init() throws NumberFormatException, IOException {
    	BufferedReader br= new BufferedReader(new InputStreamReader(System.in));;
    	nodeCnt = Integer.parseInt(br.readLine());
    	nodes = new Node[nodeCnt+1];
    	ans = 0;
    	
    	for (int i = 1; i <=nodeCnt; i++) {
    		nodes[i] = new Node();
    	}
    	
    	for (int i = 1; i <= nodeCnt; i++) {
    		StringTokenizer st = new StringTokenizer(br.readLine());
    		int cost = Integer.parseInt(st.nextToken());
    		
    		nodes[i].cost = cost;
    		
    		int parentCnt = Integer.parseInt(st.nextToken());
    		nodes[i].parentLeft = parentCnt;
    		for (int j = 0; j < parentCnt; j++) {
    			int nodeNum = Integer.parseInt(st.nextToken());
    			nodes[nodeNum].children.add(nodes[i]);
    		}
    		
    	}
    }
    
    public static void process() throws IOException {    
    	Queue<Node> q = new LinkedList<>();
    	
    	for (int i = 1; i<= nodeCnt; i++) {
    		if (nodes[i].parentLeft == 0) q.add(nodes[i]);
    	}

    	
    	while(!q.isEmpty()) {
    		Node node = q.poll();
    		
    		int newNum = node.cost + node.startTime;
    		ans = Math.max(newNum, ans);
    		
    		for (Node child: node.children) {
    			child.parentLeft--;
    			child.startTime = Math.max(child.startTime, newNum);
    			if (child.parentLeft == 0) q.add(child);
    		}
    	}
    }
    

   public static void print() {
      System.out.println(ans);
    }
}
```
