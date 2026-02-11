```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.LinkedList;
import java.util.List;
import java.util.PriorityQueue;
import java.util.Queue;

public class Main{
	private static int N, M;
	private static boolean[] isValidPoints;
	private static List<List<int[]>> graph;
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		String[] tokens = br.readLine().split(" ");
		N = Integer.parseInt(tokens[0]);
		M = Integer.parseInt(tokens[1]);
		isValidPoints = new boolean[N];
		graph = new ArrayList<>();
		tokens = br.readLine().split(" ");
		for(int i = 0; i < N; i++) {
			graph.add(new LinkedList<>());
			if ("0".equals(tokens[i]))
				isValidPoints[i] = true;
			else
				isValidPoints[i] = false;
		}
		int m = M;
		while(m-->0){
			tokens = br.readLine().split(" ");
			int s = Integer.parseInt(tokens[0]);
			int e = Integer.parseInt(tokens[1]);
			int w = Integer.parseInt(tokens[2]);
			if(s != N-1 && e != N-1){
				if(!isValidPoints[s] || !isValidPoints[e])
					continue;
			}
			graph.get(s).add(new int[]{e, w});
			graph.get(e).add(new int[]{s, w});
		}

		boolean[] visited = new boolean[N];
		long[] distances = new long[N];
		Arrays.fill(distances, Long.MAX_VALUE);
		visited[0] = true;
		distances[0] = 0;
		Queue<long[]> q = new PriorityQueue<>((o1, o2) -> Long.compare(o1[1], o2[1]));
		q.add(new long[]{0, 0});
		while(!q.isEmpty()){
			long[] element = q.poll();
			int v = (int)element[0];
			long dist = element[1];
			//System.out.println("v: %d, dis: %d".formatted(v, dist));
			if(dist > distances[v])
				continue;
			visited[v] = true;
			for(int[] nextInfo :graph.get(v)){
				int nv = nextInfo[0];
				int nw = nextInfo[1];
				if(visited[nv])
					continue;
				if(dist + nw < distances[nv]){
					distances[nv] = dist + nw;
					q.add(new long[]{nv, distances[nv]});
				}
			}
		}
		//System.out.println(Arrays.toString(distances));
		System.out.println((distances[N-1] != Long.MAX_VALUE)?distances[N-1] : -1);
		br.close();
	}
}
```
