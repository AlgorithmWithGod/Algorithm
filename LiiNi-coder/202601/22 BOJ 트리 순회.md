```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayDeque;
import java.util.Arrays;
import java.util.Deque;
import java.util.HashMap;
import java.util.Map;

public class Main {
	private static int[] BiTree;
	private static Map<Integer, Integer> TreeIdxAtValue;
	private static int answer = 0;
	private static Deque<Integer> InnerFind;
	private static Map<Integer, int[]> ChildsAtParent;
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int n = Integer.parseInt(br.readLine());
		BiTree = new int[200_010];
		InnerFind = new ArrayDeque<>();
		TreeIdxAtValue = new HashMap<>();
		ChildsAtParent = new HashMap<>();
		BiTree[1] = 1;
		TreeIdxAtValue.put(1, 1);
		int i = n;
		while(i-->0) {
			String[] temp = br.readLine().split(" ");
			int parent = Integer.parseInt(temp[0]);
			int a = Integer.parseInt(temp[1]);
			int b = Integer.parseInt(temp[2]);

			ChildsAtParent.put(parent, new int[] {a, b});
		}
		dfsTree(1, 1);
		// System.out.println(Arrays.toString(BiTree));
		//중위순회 마지막 노드 알아내기
		findLast(1);
		answer--;
		dfs(1);
		System.out.println(answer);
		br.close();
	}

	private static void dfsTree(int value, int idx){
		BiTree[idx] = value;
		int[] childValues = ChildsAtParent.get(value);
		BiTree[idx*2] = childValues[0];
		BiTree[idx*2+1] = childValues[1];
		if(childValues[0] != -1)
			dfsTree(childValues[0], idx*2);
		if(childValues[1] != -1)
			dfsTree(childValues[1], idx*2+1);
	}

	private static void findLast(int cur) {
		int a = cur*2;
		int b = cur*2+1;
		// 왼쪽자식 갈수있으면
		if(BiTree[a] != 0 && BiTree[a] != -1){
			findLast(a);
		}
		InnerFind.offerLast(cur);
		// 오른쪽자식 갈수있으면
		if(BiTree[b] != 0 && BiTree[b] != -1){
			findLast(b);
		}
	}
	private static void dfs(int cur) {
		answer++;
		int a = cur*2;
		int b = cur*2+1;
		// 왼쪽자식 갈수있으면
		if(BiTree[a] != 0 && BiTree[a] != -1){
			dfs(a);
			answer++;
		}

		// 오른쪽자식 갈수있으면
		if(BiTree[b] != 0 && BiTree[b] != -1){
			dfs(b);
			answer++;
		}

		// 유사중위 순회의 끝이라면
		if(InnerFind.getLast() == cur){
			System.out.println(answer);
			System.exit(0);
		}
	}
}
```
