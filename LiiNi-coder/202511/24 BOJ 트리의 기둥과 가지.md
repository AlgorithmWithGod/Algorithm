```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;
public class Main{
	static class Node{
		int nv;
		int w;
		Node(int nv, int w){
			this.nv = nv; this.w = w;
		}
	}
	private static int N;
	private static int R;
	private static List<List<Node>> tree;
	private static long maxLength = 0L;
	private static boolean[] visited;
	public static void main(String[] args) throws IOException {
		String[] temp;
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		temp = br.readLine().split(" ");
		N = Integer.parseInt(temp[0] );
		R = Integer.parseInt(temp[1]);

		visited = new boolean[N+1];
		tree = new ArrayList<>();
		for(int i = 0; i<N+1; i++){
			tree.add(new ArrayList<>());
		}

		for(int i = 0; i<N-1; i++){
			temp = br.readLine().split(" ");
			int v = Integer.parseInt(temp[0]);
			int nv = Integer.parseInt(temp[1] );
			int w = Integer.parseInt(temp[2]);
			tree.get(v).add(new Node(nv, w));
			tree.get(nv).add(new Node(v, w));
		}
		// 기가노드를 찾을때까지 진행
		int gigaNode = 0;
		int iterNode = R;
		int height = 0;
		while(gigaNode == 0) {
			visited[iterNode] = true;
			List<Node> nextNodes = tree.get(iterNode);
			int size = 0;
			Node nextNode = null;
			for(Node node : nextNodes){
				if(visited[node.nv]){
					continue;
				}
				size++;
				nextNode = node;
			}
			// 기둥 높이 카운트
			// if 기가노드 발견(자식이 2개이상)
			if(size > 1 || size == 0){
				// - 기둥 높이 카운트 중지 & 탈출
				gigaNode = iterNode;
				break;
			}
			height += nextNode.w;
			iterNode = nextNode.nv;
		}

		//System.out.println("height, giganode: "+ height + " " + gigaNode);
		// 기가노드에서 부터 dfs시작
		dfs(gigaNode, 0);
		System.out.println(height + " " + maxLength);
		br.close();
	}
	private static void dfs(int n, int length){
		visited[n] = true;
		List<Node> nextNodes = tree.get(n);
		if(nextNodes.size() == 1){
			// 리프 노드일때
			maxLength = Math.max(length, maxLength);
			return;
		}
		for(Node nv : tree.get(n)){
			if(visited[nv.nv]){
				continue;
			}
			dfs(nv.nv, nv.w + length);
		}
		return;
	}
}
```
