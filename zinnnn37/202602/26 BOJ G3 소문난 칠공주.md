```java
import java.io.*;

public class BJ_1941_소문난_칠공주 {

    private static final int   N    = 5;
    private static final int   SIZE = 25;
    private static final int[] dx   = { -1, 1, 0, 0 };
    private static final int[] dy   = { 0, 0, -1, 1 };

    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

    private static int         ans;
    private static boolean[]   visited;
    private static boolean[][] isS;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        isS = new boolean[N][N];
        for (int i = 0; i < N; i++) {
            String line = br.readLine();
            for (int j = 0; j < N; j++) {
                isS[i][j] = line.charAt(j) == 'S';
            }
        }
        visited = new boolean[1 << SIZE];
    }

    private static void sol() throws IOException {
        for (int i = 0; i < SIZE; i++) {
            if (!isS[i / N][i % N]) continue;

            int mask = 1 << i;

            visited[mask] = true;
            dfs(1, 1, mask);
        }

        bw.write(ans + "");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void dfs(int depth, int sCount, int mask) {
        if (7 - depth + sCount < 4) return;

        if (depth == 7) {
            ans++;
            return;
        }

        for (int i = 0; i < SIZE; i++) {
            if ((mask & (1 << i)) == 0) continue;

            int x = i / N;
            int y = i % N;

            for (int d = 0; d < 4; d++) {
                int nx = x + dx[d];
                int ny = y + dy[d];

                if (OOB(nx, ny)) continue;

                int next     = nx * N + ny;
                int nextMask = mask | (1 << next);

                if ((mask & (1 << next)) != 0) continue;
                if (visited[nextMask]) continue;

                visited[nextMask] = true;
                dfs(depth + 1, sCount + (isS[nx][ny] ? 1 : 0), nextMask);
            }
        }
    }

    private static boolean OOB(int x, int y) {
        return x < 0 || N <= x || y < 0 || N <= y;
    }

}
```