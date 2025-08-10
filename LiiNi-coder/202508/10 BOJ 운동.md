```java
import java.io.*;
import java.util.*;

public class Main {
    static class Edge {
        int to;
        int cost;
        Edge(int to, int cost) {
            this.to = to;
            this.cost = cost;
        }
    }

    private static final int INF = 1_000_000_000;//플루이드워셜은 오버플로우 방지
    private static int V
    private static int E;
    private static ArrayList<Edge>[] graph;
    private static int[][] dist;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        V = Integer.parseInt(st.nextToken());
        E = Integer.parseInt(st.nextToken());
        graph = new ArrayList[V + 1];
        for (int i = 1; i <= V; i++) {
            graph[i] = new ArrayList<>();
        }

        dist = new int[V + 1][V + 1];
        for (int i = 1; i <= V; i++) {
            Arrays.fill(dist[i], INF);
            dist[i][i] = 0;
        }

        for (int i = 0; i < E; i++) {
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            int c = Integer.parseInt(st.nextToken());
            graph[a].add(new Edge(b, c));
            dist[a][b] = c;
        }

        //플로이드워셜진행
        for (int k = 1; k <= V; k++) {
            for (int i = 1; i <= V; i++) {
                for (int j = 1; j <= V; j++) {
                    if (dist[i][j] > dist[i][k] + dist[k][j]) {
                        dist[i][j] = dist[i][k] +dist[k][j];
                    }
                }
            }
        }

        //최소 사이클 찾기
        int answer = INF;
        for (int a = 1; a <= V; a++) {
            for (int b = 1; b <= V; b++) {
                if (a == b) continue;
                if (dist[a][b] != INF && dist[b][a] != INF) {
                    answer = Math.min(answer, dist[a][b] + dist[b][a]);
                }
            }
        }

        System.out.println((answer == INF)? -1 : answer);
        br.close();
    }
}
```
