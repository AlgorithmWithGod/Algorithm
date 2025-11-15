```java
import java.util.*;

class Solution {
    static final int[] dx = {1, -1, 0, 0};
    static final int[] dy = {0, 0, 1, -1};

    public int solution(int[][] maps) {
        int n = maps.length;
        int m = maps[0].length;

        int[][] dist = new int[n][m];
        Queue<int[]> q = new ArrayDeque<>();

        dist[0][0] = 1;
        q.offer(new int[]{0, 0});

        while (!q.isEmpty()) {
            int[] cur = q.poll();
            int x = cur[0], y = cur[1];

            if (x == n - 1 && y == m - 1) {
                return dist[x][y];
            }

            for (int dir = 0; dir < 4; dir++) {
                int nx = x + dx[dir];
                int ny = y + dy[dir];

                if (nx < 0 || ny < 0 || nx >= n || ny >= m) continue;
                if (maps[nx][ny] == 0) continue;
                if (dist[nx][ny] != 0) continue;

                dist[nx][ny] = dist[x][y] + 1;
                q.offer(new int[]{nx, ny});
            }
        }

        return -1;
    }
}

```
