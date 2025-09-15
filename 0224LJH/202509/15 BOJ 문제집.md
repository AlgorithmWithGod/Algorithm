```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
	static int nodeCnt, infoCnt;
	static Node[] nodes;
	static StringBuilder sb = new StringBuilder();
	static class Node implements Comparable<Node>{
		int num;
		int beforeCnt = 0; // 이 노드 전에 나와야 하는 노드 수
		HashSet<Node> after = new HashSet<>();
		
		
		
		public Node(int num) {
			this.num = num;
		}
		
		@Override
		public int compareTo(Node n) {
			return Integer.compare(this.num, n.num);
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
    	nodeCnt =Integer.parseInt(st.nextToken());
    	infoCnt = Integer.parseInt(st.nextToken());
    	nodes = new Node[nodeCnt+1];
    	
    	for (int i = 1 ; i <= nodeCnt; i++) nodes[i] = new Node(i);
    	for (int i = 0; i < infoCnt; i++) {
    		st = new StringTokenizer(br.readLine());
    		int before = Integer.parseInt(st.nextToken());
    		int after = Integer.parseInt(st.nextToken());
    		
    		nodes[after].beforeCnt++;
    		nodes[before].after.add(nodes[after]);
    	}

    }
    
    public static void process() {   
    	PriorityQueue<Node> pq = new PriorityQueue<>();
    	for (int i = 1; i<= nodeCnt; i++) {
    		if (nodes[i].beforeCnt != 0 )continue;
    		pq.add(nodes[i]);
    	}
    	
    	while(!pq.isEmpty()) {
    		Node n =pq.poll();
    		if ( n.beforeCnt != 0) {
    			pq.add(n);
    			continue;
    		}
    		
    		sb.append(n.num).append(" ");
    		
    		for (Node b: n.after) {
    			b.beforeCnt--;
    			if (b.beforeCnt == 0) pq.add(b);
    		}
    	}
    	
    }


	public static void print() {
    	System.out.println(sb.toString());
    }
}
```
