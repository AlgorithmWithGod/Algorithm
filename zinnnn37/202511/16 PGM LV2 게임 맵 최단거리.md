```java
import java.util.ArrayDeque;
import java.util.Queue;

public class PGM_LV2_게임_맵_최단거리 {

    private static final int[] dx = { 0, 1, 0, -1 };
    private static final int[] dy = { 1, 0, -1, 0 };

    private static int N, M;
    private static int[][]      map;
    private static boolean[][]  visited;
    private static Queue<Point> q;

    private static class Point {

        int x;
        int y;
        int cnt;

        Point(int x, int y, int cnt) {
            this.x = x;
            this.y = y;
            this.cnt = cnt;
        }

    }

    private static boolean OOB(int x, int y) {
        return x < 0 || N <= x || y < 0 || M <= y;
    }

    private static int bfs() {
        q.offer(new Point(0, 0, 1));
        visited[0][0] = true;

        while (!q.isEmpty()) {
            Point cur = q.poll();

            if (cur.x == N - 1 && cur.y == M - 1) return cur.cnt;

            for (int d = 0; d < 4; d++) {
                int nx = cur.x + dx[d];
                int ny = cur.y + dy[d];

                if (OOB(nx, ny) || visited[nx][ny] || map[nx][ny] == 0) continue;

                q.offer(new Point(nx, ny, cur.cnt + 1));
                visited[nx][ny] = true;
            }
        }

        return -1;
    }

    public int solution(int[][] maps) {
        N = maps.length;
        M = maps[0].length;

        map = maps;
        visited = new boolean[N][M];
        q = new ArrayDeque<>();

        return bfs();
    }

}
```