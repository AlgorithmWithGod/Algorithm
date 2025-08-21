```java
import java.util.*;
import java.io.*;

public class boj1956 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
    static int nextInt() {return Integer.parseInt(st.nextToken());}
    static final int INF = 987654321;

    public static void main(String[] args) throws Exception {
        nextLine();
        int V = nextInt();
        int E = nextInt();
        int[][] dist = new int[V+1][V+1];
        int answer = INF;
        for (int i = 0; i <= V; i++) {
            Arrays.fill(dist[i], INF);
            dist[i][i] = 0;
        }
        for (int i = 0; i < E; i++) {
            nextLine();
            int a = nextInt();
            int b = nextInt();
            int c = nextInt();
            dist[a][b] = c;
        }
        for (int k = 1; k <= V; k++) {
            for (int i = 1; i <= V; i++) {
                for (int j = 1; j <= V; j++) {
                    if (dist[i][j] > dist[i][k] + dist[k][j]) {
                        dist[i][j] = dist[i][k] + dist[k][j];
                    }
                }
            }
        }
        for (int i = 1; i <= V; i++) {
            for (int j = 1; j <= V; j++) {
                if (dist[i][j] == INF || dist[j][i] == INF) continue;
                if (i == j) continue;
                answer = Math.min(answer, dist[i][j] + dist[j][i]);
            }
        }
        if (answer == INF) System.out.println(-1);
        else System.out.println(answer);
    }
}
```
