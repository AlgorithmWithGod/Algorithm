```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main{
	private static int M;
	private static int N;
	private static List<int[]> Edges;
	private static int sumEdge;
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		String[] temp;
		while(true){
			temp = br.readLine().split(" ");
			M = Integer.parseInt(temp[0]);
			N = Integer.parseInt(temp[1] );
			if(M == 0 && N == 0){
				break;
			}
			Edges = new ArrayList<>();
			sumEdge = 0;
			int n = N;
			while(n-->0){
				temp = br.readLine().split(" ");
				sumEdge += Integer.parseInt(temp[2]);
				Edges.add(new int[]{
					Integer.parseInt(temp[0]),
					Integer.parseInt(temp[1]),
					Integer.parseInt(temp[2])
				});
			}
			solve();
			System.out.println(sumEdge);
		}
	}

	private static void solve() {
		List<List<int[]>> graph = new ArrayList<>();
		for(int i = 0; i < M; i++)
			graph.add(new ArrayList<>());
		for(int[] edge : Edges){
			graph.get(edge[0]).add(new int[]{edge[1], edge[2]});
			graph.get(edge[1]).add(new int[]{edge[0], edge[2]});
		}
		//프림
		Queue<int[]> q = new PriorityQueue<>((o1, o2) -> o1[1] - o2[1]);
		boolean[] visited = new boolean[M];
		int visitedCount = 1;
		visited[0] = true;
		for(int[] next : graph.get(0)){
			int nv = next[0];
			int w = next[1];
			q.offer(new int[]{nv, w});
		}
		while(visitedCount < M){
			// -- 최소힙에서 팝
			int[] temp = q.poll();
			int nv = temp[0];
			int w = temp[1];
			// -- 만약 다음 정점번호가 방문이면 컨티뉴
			if(visited[nv])
				continue;
			// 방문여부 표시
			visited[nv] =true;
			visitedCount++;
			// -- 스패닝 트리 간선 처리
			sumEdge -= w;
			for(int[] next : graph.get(nv)){
				int nnv = next[0];
				if(visited[nnv])
					continue;
				int nw = next[1];
				q.offer(new int[]{nnv, nw});
			}
			// -- 최소힙에 푸시
		}
	}
}
```
