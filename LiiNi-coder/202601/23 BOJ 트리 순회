```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayDeque;
import java.util.Deque;
import java.util.HashMap;
import java.util.Map;

public class Main{

	private static class Node{
		int value;
		Node c1;
		Node c2;
		public Node(int v){
			this.value = v;
			c1 = c2 = null;
		}
	}
	private static Map<Integer, Node> Nodes;
	private static long answer = 0;
	private static Deque<Integer>  q = new ArrayDeque<>();
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int n = Integer.parseInt(br.readLine());
		int t = n;
		Nodes = new HashMap<>();
		Nodes.put(1, new Node(1));
		while(t-->0){
			String[] tokens = br.readLine().split(" ");
			int parentValue = Integer.parseInt(tokens[0 ]);
			Node parentNode = Nodes.get(parentValue);
			if(parentNode == null){
				parentNode = new Node(parentValue);
				Nodes.put(parentValue, parentNode);
			}

			int child1Value = Integer.parseInt(tokens[1]);
			if(child1Value != -1){
				Node child1Node = Nodes.get(child1Value);
				if(child1Node == null){
					child1Node = new Node(child1Value);
					Nodes.put(child1Value, child1Node);
				}
				parentNode.c1 = child1Node;
			}
			int child2Value = Integer.parseInt(tokens[2 ]);
			if(child2Value != -1){
				Node child2Node = Nodes.get(child2Value);
				if(child2Node == null){
					child2Node = new Node(child2Value);
					Nodes.put(child2Value, child2Node);
				}
				parentNode.c2 = child2Node;
			}
		}
		findLastNode(Nodes.get(1));
		answer--;
		dfs(Nodes.get(1));
		br.close();
	}

	private static void dfs(Node cur) {
		answer++;
		if(cur.c1 != null){
			dfs(cur.c1);
			answer++;
		}
		if(q.getLast() == cur.value){
			System.out.println(answer++);
			System.exit(0);
		}
		if(cur.c2 != null){
			dfs(cur.c2);
			answer++;
		}
	}

	private static void findLastNode(Node cur) {
		if(cur.c1 != null){
			findLastNode(cur.c1);
		}
		q.offerLast(cur.value);
		if(cur.c2 != null){
			findLastNode(cur.c2);
		}
	}
}
```
