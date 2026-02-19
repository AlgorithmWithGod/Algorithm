```java
import java.io.*;
import java.util.*;

public class Main {

    static int N;
    static double[] probs = new double[4];
    static boolean[][] visited = new boolean[30][30];
    static int[] dr = {0, 0, 1, -1};
    static int[] dc = {1, -1, 0, 0};
    static double totalProb = 0;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        for (int i = 0; i < 4; i++) {
            probs[i] = Integer.parseInt(st.nextToken()) * 0.01;
        }

        visited[15][15] = true;
        dfs(15, 15, 0, 1.0);

        System.out.println(totalProb);
    }

    static void dfs(int r, int c, int cnt, double currentProb) {
        if (cnt == N) {
            totalProb += currentProb;
            return;
        }

        for (int i = 0; i < 4; i++) {
            if (probs[i] == 0) continue;

            int nr = r + dr[i];
            int nc = c + dc[i];

            if (!visited[nr][nc]) {
                visited[nr][nc] = true;
                dfs(nr, nc, cnt + 1, currentProb * probs[i]);
                visited[nr][nc] = false;
            }
        }
    }
}
```
