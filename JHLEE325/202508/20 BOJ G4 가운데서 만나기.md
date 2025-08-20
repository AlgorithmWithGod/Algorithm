```java
import java.io.*;
import java.util.*;

public class Main {

    static int n, m, k;
    static int[][] map;
    static final int INF = 987654321;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());

        map = new int[n][n];
        for (int i = 0; i < n; i++) {
            Arrays.fill(map[i], INF);
            map[i][i] = 0;
        }

        for (int i = 0; i < m; i++) {
            st = new StringTokenizer(br.readLine());
            int from = Integer.parseInt(st.nextToken()) - 1;
            int to = Integer.parseInt(st.nextToken()) - 1;
            int cost = Integer.parseInt(st.nextToken());
            if (cost < map[from][to]) map[from][to] = cost;
        }

        for (int k = 0; k < n; k++) {
            for (int i = 0; i < n; i++) {
                if (map[i][k] == INF) continue;
                for (int j = 0; j < n; j++) {
                    if (map[k][j] == INF) continue;
                    map[i][j] = Math.min(map[i][j], map[i][k] + map[k][j]);
                }
            }
        }

        k = Integer.parseInt(br.readLine());
        int[] friend = new int[k];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < k; i++) {
            friend[i] = Integer.parseInt(st.nextToken()) - 1;
        }

        int best = INF;
        ArrayList<Integer> ans = new ArrayList<>();

        for (int v = 0; v < n; v++) {
            int worst = 0;
            boolean ok = true;
            for (int s : friend) {
                if (map[s][v] == INF || map[v][s] == INF) {
                    ok = false;
                    break;
                }
                worst = Math.max(worst, map[s][v] + map[v][s]);
            }
            if (!ok) continue;

            if (worst < best) {
                best = worst;
                ans.clear();
                ans.add(v + 1);
            } else if (worst == best) {
                ans.add(v + 1);
            }
        }

        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < ans.size(); i++) {
            if (i > 0) sb.append(' ');
            sb.append(ans.get(i));
        }
        System.out.println(sb.toString());
    }
}

```
