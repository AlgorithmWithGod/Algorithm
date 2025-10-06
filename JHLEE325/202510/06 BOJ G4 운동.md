```java
import java.io.*;
import java.util.*;

public class Main {

    static final int INF = 987654321;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int v = Integer.parseInt(st.nextToken());
        int e = Integer.parseInt(st.nextToken());

        int[][] map = new int[v][v];

        for (int i = 0; i < v; i++) {
            Arrays.fill(map[i], INF);
        }

        for (int i = 0; i < e; i++) {
            st = new StringTokenizer(br.readLine());
            int s = Integer.parseInt(st.nextToken()) - 1;
            int d = Integer.parseInt(st.nextToken()) - 1;
            int c = Integer.parseInt(st.nextToken());

            map[s][d] = c;
        }

        for (int k = 0; k < v; k++) {
            for (int i = 0; i < v; i++) {
                for (int j = 0; j < v; j++) {
                    map[i][j] = Math.min(map[i][j], map[i][k] + map[k][j]);
                }
            }
        }
        int res = INF;
        for (int i = 0; i < v; i++) {
            for (int j = 0; j < v; j++) {
                res = Math.min(res, map[i][j] + map[j][i]);
            }
        }

        if (res == INF) {
            System.out.println(-1);
        } else {
            System.out.println(res);
        }
    }
}
```
