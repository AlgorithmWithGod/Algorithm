```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
    private static BufferedReader br;
    private static StringTokenizer st;
    private static int n;
    private static int m;
    private static int r;
    private static int[][] dist;
    private static int[] items;
    private static final int INF = 1_000_000;

    public static void main(String[] args) throws IOException {
        br = new BufferedReader(new InputStreamReader(System.in));
        String[] temp = br.readLine().split(" ");
        n = Integer.parseInt(temp[0]);
        m = Integer.parseInt(temp[1]);
        r = Integer.parseInt(temp[2]);
        items = new int[n + 1];
        st = new StringTokenizer(br.readLine());
        for (int i = 1; i <= n; i++) {
            items[i] = Integer.parseInt(st.nextToken());
        }
        
        dist = new int[n + 1][n + 1];
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= n; j++) {
                if (i == j) dist[i][j] = 0;
                else dist[i][j] = INF;
            }
        }
        for (int i = 0; i < r; i++) {
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            int c = Integer.parseInt(st.nextToken());
            dist[a][b] = Math.min(dist[a][b], c);
            dist[b][a] = Math.min(dist[b][a], c);
        }
        //플로이드-워셜
        for (int k = 1; k <= n; k++) {
            for (int i = 1; i <= n; i++) {
                for (int j = 1; j <= n; j++) {
                    if (dist[i][k] != INF && dist[k][j] != INF) {
                        dist[i][j] = Math.min(dist[i][j], dist[i][k] + dist[k][j]);
                    }
                }
            }
        }
        
        int maxItems = 0;
        for (int i = 1; i <= n; i++) {
            int currentItems = 0;
            for (int j = 1; j <= n; j++) {
                if (dist[i][j] <= m) {
                    currentItems += items[j];
                }
            }
            maxItems = Math.max(maxItems, currentItems);
        }
        System.out.println(maxItems);
    }
}
```
