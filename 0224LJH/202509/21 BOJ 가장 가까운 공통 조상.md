```java

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

class Main {
	static BufferedReader br= new BufferedReader(new InputStreamReader(System.in));
	static int nodeCnt, num1, num2,ans;
	static Node[] nodes;
	static HashSet<Node> set = new HashSet<>();
	
	static class Node{
		int num;
		Node parent;
		HashSet<Node> children = new HashSet<>();

	}
	
    
    public static void main(String[] args) throws NumberFormatException, IOException {
		int TC = Integer.parseInt(br.readLine());
		for (int tc = 1; tc <= TC; tc++) {
	        init();
	    	process();
	    	print();

		}

    }

    
    public static void init() throws NumberFormatException, IOException {
    	
    	nodeCnt = Integer.parseInt(br.readLine());
    	nodes = new Node[nodeCnt+1];
    	
    	for (int i = 1; i <= nodeCnt; i++) {
    		nodes[i] = new Node();
    		nodes[i].num = i;
    	}
    	
    	for (int i = 0; i < nodeCnt-1; i++) {
    		StringTokenizer st = new StringTokenizer(br.readLine());
    		int parentNum = Integer.parseInt(st.nextToken());
    		int childNum = Integer.parseInt(st.nextToken());
    		
    		nodes[parentNum].children.add(nodes[childNum]);
    		nodes[childNum].parent = nodes[parentNum];
    	}
    	
    	StringTokenizer st = new StringTokenizer(br.readLine());
    	num1 = Integer.parseInt(st.nextToken());
    	num2 = Integer.parseInt(st.nextToken());
    	
    	

    }
    
    public static void process() { 	
    	set.clear();
    	
    	Node cur = nodes[num1];
    	set.add(cur);
    	while(cur.parent != null) {
    		set.add(cur);
    		cur = cur.parent;
    	}
    	
    	cur = nodes[num2];
    	while(cur.parent != null) {
    		if (set.contains(cur)) {
    			ans = cur.num;
    			return;
    		}
    		cur = cur.parent;
    	}
    	
    	ans = cur.num;
    	
    }




	public static void print() {
		System.out.println(ans);
    }
}
```
