```java
import java.io.*;
import java.util.*;

public class Main {

    static char[][] map = new char[12][6];
    static int[] dr = {-1, 1, 0, 0};
    static int[] dc = {0, 0, -1, 1};
    static boolean isPopped;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        for (int i = 0; i < 12; i++) {
            map[i] = br.readLine().toCharArray();
        }

        int chainCount = 0;
        while (true) {
            isPopped = false;
            boolean[][] visited = new boolean[12][6];

            for (int i = 0; i < 12; i++) {
                for (int j = 0; j < 6; j++) {
                    if (map[i][j] != '.' && !visited[i][j]) {
                        bfs(i, j, visited);
                    }
                }
            }

            if (!isPopped) break;

            fall();
            chainCount++;
        }

        System.out.println(chainCount);
    }

    static void bfs(int r, int c, boolean[][] visited) {
        List<int[]> puyos = new ArrayList<>();
        Queue<int[]> q = new LinkedList<>();
        char color = map[r][c];

        q.add(new int[]{r, c});
        puyos.add(new int[]{r, c});
        visited[r][c] = true;

        while (!q.isEmpty()) {
            int[] cur = q.poll();

            for (int i = 0; i < 4; i++) {
                int nr = cur[0] + dr[i];
                int nc = cur[1] + dc[i];

                if (nr >= 0 && nr < 12 && nc >= 0 && nc < 6) {
                    if (!visited[nr][nc] && map[nr][nc] == color) {
                        visited[nr][nc] = true;
                        q.add(new int[]{nr, nc});
                        puyos.add(new int[]{nr, nc});
                    }
                }
            }
        }

        if (puyos.size() >= 4) {
            for (int[] p : puyos) {
                map[p[0]][p[1]] = '.';
            }
            isPopped = true;
        }
    }

    static void fall() {
        for (int c = 0; c < 6; c++) {
            for (int r = 11; r > 0; r--) {
                if (map[r][c] == '.') {
                    for (int k = r - 1; k >= 0; k--) {
                        if (map[k][c] != '.') {
                            map[r][c] = map[k][c];
                            map[k][c] = '.';
                            break;
                        }
                    }
                }
            }
        }
    }
}
```
