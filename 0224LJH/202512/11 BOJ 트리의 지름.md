```java

import java.util.StringTokenizer;
import java.util.*;
import java.io.*;

public class Main {
	
	static int nodeCnt,ans = 0;
	static Node[] nodes;
	
	static class Node{
		int idx = 0;
		Node parent = null;
		HashSet<Node> set = new HashSet<>();
		int dis = 0;
		
		public Node (int idx) {
			this.idx = idx;
		}
	}

	

    public static void main(String[] args) throws IOException {
    	init();
    	process();
    	print();

    }
    
    private static void init() throws IOException{
    	BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    	nodeCnt = Integer.parseInt(br.readLine());
    	nodes = new Node[nodeCnt+1];
    	
    	for (int i = 1; i<= nodeCnt; i++) {
    		nodes[i] = new Node(i);
    	}
    	
    	for (int i = 1; i < nodeCnt; i++) {
    		StringTokenizer st = new StringTokenizer(br.readLine());
    		int pNum = Integer.parseInt(st.nextToken());
    		int cNum = Integer.parseInt(st.nextToken());
    		int dis = Integer.parseInt(st.nextToken());
    		Node p = nodes[pNum];
    		Node c = nodes[cNum];
    		c.parent = p;
    		p.set.add(c);
    		c.dis = dis;
    	}
    }
    
    private static void process() throws IOException {
    	int rs = recursive(1);
    	ans = Math.max(ans, rs);
    	
    }
    
    public static int recursive(int num) {
    	Node target = nodes[num];
    	if(target.set.isEmpty()) return target.dis;
    	
    	PriorityQueue<Integer> pq = new PriorityQueue<>(Collections.reverseOrder());
    	
    	for (Node n: target.set) {
    		pq.add(recursive(n.idx));
    	}
    	int longest = pq.poll();
    	
    	if (!pq.isEmpty()) {
    		int second = pq.poll();
    		
    		ans = Math.max(ans, longest+second);
    	}
    	
    	
    	return longest + target.dis;
    }
    
   private static void print() {
      System.out.println(ans);
    }

}
```
