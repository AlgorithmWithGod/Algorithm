```java
import java.util.*;
import java.io.*;

public class Main {

    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static int V,E;
    static int[][] matrix;
    static int INF = 1000000007;
    static int ans = INF;

    public static void main(String[] args) throws Exception {
        st = new StringTokenizer(br.readLine());
        V = Integer.parseInt(st.nextToken());
        E = Integer.parseInt(st.nextToken());

        matrix = new int[V+1][V+1];
        for (int i = 0; i <= V; i++) {
            for (int j = 0; j <= V; j++) {
                if(i != j) {
                    matrix[i][j] = INF;
                }
            }
        }

        for (int i = 0; i < E; i++) {
            st = new StringTokenizer(br.readLine());
            int from = Integer.parseInt(st.nextToken());
            int to = Integer.parseInt(st.nextToken());
            int cost = Integer.parseInt(st.nextToken());
            matrix[from][to] = cost;
        }

        for (int k = 1; k <= V; k++) for (int i = 1; i <= V; i++) for (int j = 1; j <= V; j++) {
            matrix[i][j] = Math.min(matrix[i][j], matrix[i][k] + matrix[k][j]);
        }

        for (int i = 1; i <= V; i++) for (int j = 1; j <= V; j++) {
            if(i != j) ans = Math.min(ans, matrix[i][j] + matrix[j][i]);
        }

        System.out.println(ans >= INF ? -1 : ans);
    }
}
```
