```java
import java.io.*;
import java.util.*;

public class Main {
    static int n, m, h, c;
    static List<int[]> houses = new ArrayList<>();
    static List<int[]> chickens = new ArrayList<>();
    static int[][] dist;
    static int[] pick;
    static int answer = Integer.MAX_VALUE;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());

        for (int i = 0; i < n; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < n; j++) {
                int v = Integer.parseInt(st.nextToken());
                if (v == 1) houses.add(new int[]{i, j});
                else if (v == 2) chickens.add(new int[]{i, j});
            }
        }

        h = houses.size();
        c = chickens.size();

        dist = new int[h][c];
        for (int h = 0; h < Main.h; h++) {
            int hx = houses.get(h)[0], hy = houses.get(h)[1];
            for (int k = 0; k < Main.c; k++) {
                int cx = chickens.get(k)[0], cy = chickens.get(k)[1];
                dist[h][k] = Math.abs(hx - cx) + Math.abs(hy - cy);
            }
        }

        pick = new int[m];
        dfs(0, 0);

        System.out.println(answer);
    }

    static void dfs(int start, int depth) {
        if (depth == m) {
            int sum = 0;
            for (int h = 0; h < Main.h; h++) {
                int best = Integer.MAX_VALUE;
                for (int p = 0; p < m; p++) {
                    best = Math.min(best, dist[h][pick[p]]);
                }
                sum += best;
                if (sum >= answer) return;
            }
            answer = Math.min(answer, sum);
            return;
        }

        for (int i = start; i < c; i++) {
            pick[depth] = i;
            dfs(i + 1, depth + 1);
        }
    }
}

```
