```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.List;
import java.util.PriorityQueue;

public class Main{
	// 크루스칼 -> 간선 중심 -> 간선이 적을때 쓰면 좋음 -> disjoint set알고리즘 구현 필요
	// 프림 -> 정점 중심 -> MST와 우선숭위큐에 정점을 넣어가며 그 예비 MST의 간선을 선택해나가는것
	static int N, M;
	static List<List<int[]>> Graph;
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		String[] tokens = br.readLine().split(" ");
		N = Integer.parseInt(tokens[0]);
		M = Integer.parseInt(tokens[1]);
		int m = M;
		Graph = new ArrayList<>();
		for(int i = 0; i <= N; i++){
			Graph.add(new ArrayList<>());
		}
		long overSum = 0L;
		while(m-->0){
			tokens = br.readLine().split(" ");
			int s = Integer.parseInt(tokens[0]);
			int e = Integer.parseInt(tokens[1]);
			int w = Integer.parseInt(tokens[2]);
			overSum += w;
			Graph.get(s).add(new int[]{e, w});
			Graph.get(e).add(new int[]{s, w});
		}

		boolean[] visited = new boolean[N+1];
		var q = new PriorityQueue<int[]>((o1, o2)->o1[1] - o2[1]);
		q.add(new int[]{1, 0});
		long mstSum = 0L;

		while(!q.isEmpty()){
			var qItem = q.poll();
			int v = qItem[0]; int w = qItem[1];
			if(visited[v]) continue;
			visited[v] = true;
			mstSum += w;
			for(int[] nextInfo : Graph.get(v)){
				int nv = nextInfo[0]; int nw = nextInfo[1];
				if(visited[nv]) continue;
				q.add(new int[]{nv, nw});
			}
		}
		for(int i = 1; i < N+1; i++){
			if(!visited[i]){
				System.out.println(-1);
				return;
			}
		}
		System.out.println(overSum - mstSum);
		br.close();
	}
}
```
