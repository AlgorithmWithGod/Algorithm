```java
import java.util.*;
import java.io.*;
public class Main{
	/*
	* 순서 그래프 생성
	* 간선 최적화 안하고 그냥 바로 최단거리 알고리즘 돌림
	*
	* */
	private static List<List<Integer>> Graph;
	private static int N, M;
	private static int MAX = Integer.MAX_VALUE / 2;
	public static void main(String[] args) throws IOException{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		N = Integer.parseInt(st.nextToken());
		M = Integer.parseInt(st.nextToken());
		Graph = new ArrayList<>();
		for(int i = 0; i < N; i++) Graph.add(new ArrayList<>());
		for(int i = 0; i < M; i++){
			st = new StringTokenizer(br.readLine());
			int s = Integer.parseInt(st.nextToken()) - 1;
			int e = Integer.parseInt(st.nextToken()) - 1;

			Graph.get(s).add(e);
		}

		//인접리스트 -> 인접행렬
		int[][] dists = new int[N][N];
		for(int r = 0; r < N; r++)
			for(int c = 0; c < N; c++)
				dists[r][c] = MAX;
		for(int s = 0; s < N; s++){
			for(int e : Graph.get(s)){
				dists[s][e] = 1;
			}
		}
		for(int i = 0; i < N; i++)
			dists[i][i] = 0;

		//플로이드워셜
		for(int k = 0; k < N; k++)
			for(int s = 0; s < N; s++)
				for(int e = 0; e < N; e++){
					int nw = dists[s][k] + dists[k][e];
					if(nw < dists[s][e])
						dists[s][e] = nw;
				}

		// for(int[] row : dists)
		// 	System.out.println(Arrays.toString(row));
		int query = Integer.parseInt(br.readLine());
		for(int i = 0; i < query; i++){
			st = new StringTokenizer(br.readLine());
			int l = Integer.parseInt(st.nextToken()) - 1;
			int r = Integer.parseInt(st.nextToken()) -1;

			boolean lr = (dists[l][r] > 0 && dists[l][r] < MAX);
			boolean rl = (dists[r][l] > 0 && dists[r][l] < MAX );
			// System.out.println(lr + ", " + rl);
			String answer;
			if(lr)
				answer = "-1";
			else if(rl)
				answer = "1";
			else
				answer = "0";
			System.out.println(answer);
		}

		br.close();
	}
}
```
