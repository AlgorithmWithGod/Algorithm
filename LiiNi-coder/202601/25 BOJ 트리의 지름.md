```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayDeque;
import java.util.ArrayList;
import java.util.Deque;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

import org.w3c.dom.Node;

public class Main{
	private static int N;
	private static Map<Integer, List<int[]>> Graph = new HashMap<Integer, List<int[]>>();
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in ));
		N = Integer.parseInt(br.readLine());
		int t = N;
		while(t-- > 1){
			String[] tokens = br.readLine().split(" ");
			int parent = Integer.parseInt(tokens[0] );
			int child = Integer.parseInt(tokens[1]);
			int weight = Integer.parseInt(tokens[2] );
			Graph.putIfAbsent(parent, new ArrayList<int[]>());
			Graph.get(parent).add(new int[]{child, weight});
			Graph.putIfAbsent(child, new ArrayList<int[]>());
			Graph.get(child).add(new int[]{parent, weight});
		}
		if(N == 1){
			System.out.println(0);
		}else{
			int[] temp = bfs(1);
			temp = bfs(temp[0]);
			System.out.println(temp[1] );

		}
		br.close();
	}

	private static int[] bfs(int start) {
		Deque<int[]> q = new ArrayDeque<int[]>();
		boolean[] visited = new boolean[10_001];
		visited[start] = true;
		int maxDist = 0;
		int nodeHavingMaxDist = 0;
		q.offer(new int[]{start, 0});
		while(!q.isEmpty()){
			int[] qItem = q.poll();
			int v = qItem[0];
			int dist = qItem[1];
			for(int[] nextInfo : Graph.get(v)){
				int nv = nextInfo[0];
				int weight = nextInfo[1];
				if(visited[nv])
					continue;
				q.offer(new int[]{nv, dist + weight});
				visited[nv] = true;
			}
			if (maxDist < dist) {
				nodeHavingMaxDist = v;
				maxDist = Math.max(maxDist, dist);
			}
		}
		return new int[]{nodeHavingMaxDist, maxDist};
	}
}
```
