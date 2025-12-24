```java
import java.io.*;
import java.util.*;

public class Main {
	static final int INF = 1_000_000_000;

	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int N = Integer.parseInt(br.readLine());
		int M = Integer.parseInt(br.readLine());
		int[][] dist = new int[N + 1][N + 1];
		for(int i = 1; i <= N; i++){
			for(int j = 1; j <= N; j++){
				if(i == j){
					dist[i][j] = 0;
				} else {
					dist[i][j] = INF;
				}
			}
		}

		for(int i = 0; i < M; i++){
			StringTokenizer st = new StringTokenizer(br.readLine());
			int s = Integer.parseInt(st.nextToken());
			int e = Integer.parseInt(st.nextToken());
			int w = Integer.parseInt(st.nextToken());
			dist[s][e] = Math.min(dist[s][e], w);
		}
		//플루이드워셜
		for(int k = 1; k <= N; k++){
			for(int i = 1; i <= N; i++){
				for(int j = 1; j <= N; j++){
					if(dist[i][j] > dist[i][k] + dist[k][j]){
						dist[i][j] = dist[i][k] + dist[k][j];
					}
				}
			}
		}
		
		StringBuilder sb = new StringBuilder();
		for(int i = 1; i <= N; i++){
			for(int j = 1; j <= N; j++){
				if(dist[i][j] == INF){
					sb.append(0).append(" ");
				} else {
					sb.append(dist[i][j]).append(" ");
				}
			}
			sb.append("\n");
		}
		System.out.println(sb.toString());
	}
}

```
