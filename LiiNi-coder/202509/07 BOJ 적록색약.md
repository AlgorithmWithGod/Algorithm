```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayDeque;

public class Main {
    private static final int[] dr = {-1, 0, 1, 0};
    private static final int[] dc = {0, 1, 0, -1};

    public static void main(String[] args) throws IOException {
        var br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        char[][] normal = new char[n][n];
        char[][] weak = new char[n][n];
        for (int i = 0; i < n; i++) {
            String line = br.readLine();
            for (int j = 0; j < n; j++) {
                char c = line.charAt(j);
                normal[i][j] = c;
                weak[i][j] = (c == 'G') ? 'R' : c;
            }
        }
        int normalCount = countAreas(normal, n);
        int weakCount = countAreas(weak, n);

        System.out.printf("%d %d\n", normalCount, weakCount);
    }
    private static int countAreas(char[][] map, int n) {
        boolean[][] visited = new boolean[n][n];
        int count = 0;
        var queue = new ArrayDeque<int[]>();

        for (int r = 0; r < n; r++) {
            for (int c = 0; c < n; c++) {
                if (visited[r][c])
                    continue;
                char color = map[r][c];
                count++;
                visited[r][c] = true;
                queue.offer(new int[] {r, c});
                while (!queue.isEmpty()) {
                    int[] now = queue.poll();
                    for (int d = 0; d < 4; d++) {
                        int nr = now[0] + dr[d];
                        int nc = now[1] + dc[d];
                        if (nr >= 0 && nr < n && nc >= 0 && nc < n
                            && !visited[nr][nc]
                            && map[nr][nc] == color) {
                            visited[nr][nc] = true;
                            queue.offer(new int[] {nr, nc});
                        }
                    }
                }
            }
        }
        return count;
    }
}
```
