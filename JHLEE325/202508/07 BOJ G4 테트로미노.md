```java
import java.io.*;
import java.util.*;

public class Main {

    static int n, m;
    static int[][] board;
    static boolean[][] visited;
    static int max = 0;

    static final int[][] dir = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        st = new StringTokenizer(br.readLine());
        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());
        board = new int[n][m];
        visited = new boolean[n][m];

        for (int r = 0; r < n; r++) {
            st = new StringTokenizer(br.readLine());
            for (int c = 0; c < m; c++) {
                board[r][c] = Integer.parseInt(st.nextToken());
            }
        }

        for (int r = 0; r < n; r++) {
            for (int c = 0; c < m; c++) {
                visited[r][c] = true;
                dfs(r, c, board[r][c], 1);
                visited[r][c] = false;

                chkother(r, c);
            }
        }

        System.out.println(max);
    }

    static void dfs(int x, int y, int sum, int depth) {
        if (depth == 4) {
            max = Math.max(max, sum);
            return;
        }

        for (int d = 0; d < 4; d++) {
            int nx = x + dir[d][0];
            int ny = y + dir[d][1];

            if (nx < 0 || ny < 0 || nx >= n || ny >= m || visited[nx][ny]) continue;

            visited[nx][ny] = true;
            dfs(nx, ny, sum + board[nx][ny], depth + 1);
            visited[nx][ny] = false;
        }
    }

    static void chkother(int x, int y) {
        int wing = 0;
        int min = Integer.MAX_VALUE;
        int sum = board[x][y];

        for (int d = 0; d < 4; d++) {
            int nx = x + dir[d][0];
            int ny = y + dir[d][1];

            if (nx < 0 || ny < 0 || nx >= n || ny >= m) continue;
            wing++;
            sum += board[nx][ny];
            min = Math.min(min, board[nx][ny]);
        }

        if (wing < 3) return;
        if (wing == 4) sum -= min;
        max = Math.max(max, sum);
    }
}

```
