```java

import java.util.StringTokenizer;
import java.util.*;
import java.io.*;

public class Main {
	
	static int nodeCnt,ans;
	static Node[] nodes;
	static Node root;
   
   static class Node {
	   Node parent;
	   boolean alive = true;
	   Set<Node> children = new HashSet<>();
	   
	   public void checkLeaf() {
		   int childCnt = 0;
		   for (Node n: children) {
			   if (!n.alive) continue;
			   childCnt++;
			   n.checkLeaf();
		   }
		   if (childCnt==0) ans++;
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
    	ans = 0;
    	
    	nodes = new Node[nodeCnt];
    	for (int i = 0; i < nodeCnt; i++) {
    		nodes[i] = new Node();
    	}
    	StringTokenizer st = new StringTokenizer(br.readLine());
    	for (int i = 0; i < nodeCnt; i++) {
    		int parent = Integer.parseInt(st.nextToken());
    		if (parent == -1) {
    			root = nodes[i];
    			continue;
    		}
    		Node p = nodes[parent];
    		nodes[i].parent = p;
    		p.children.add(nodes[i]);
    	}
    	
    	int targetNum = Integer.parseInt(br.readLine());
    	Node target = nodes[targetNum];
    	target.alive = false;
    
    }
    
    private static void process() throws IOException {
    	if (root.alive) root.checkLeaf();

    }
    
   private static void print() {
      System.out.println(ans);
    }

}
```
