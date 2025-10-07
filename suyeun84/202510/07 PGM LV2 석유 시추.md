```java
import java.util.*;
class Solution {
    static int[][] visited;
    static int[][] dir = new int[][] {{1,0},{-1,0},{0,1},{0,-1}};
    static int N, M, answer;

    static int id;
    static int[] size;

    public int solution(int[][] land) {
        answer = 0;
        N = land.length;
        M = land[0].length;
        visited = new int[N][M];
        size = new int[N * M + 1];
        id = 0;

        // 0 : 빈 땅, 1 : 석유가 있는 땅
        for (int j = 0; j < M; j++) {
            int total = 0;
            Set<Integer> used = new HashSet<>();
            for (int i = 0; i < N; i++) {
                if (land[i][j] == 0) continue;
                if (visited[i][j] == 0) {
                    id++;
                    bfs(i, j, land);
                }
                int comp = visited[i][j];
                if (!used.contains(comp)) {
                    used.add(comp);
                    total += size[comp];
                }
                int ny = i;
                while (i < N && land[i][j] == 1) i++;
                if (i != N) i--;
            }
            answer = Math.max(answer, total);
        }
        return answer;
    }

    private void bfs(int i, int j, int[][] land) {
        Queue<Point> q = new LinkedList<>();
        q.add(new Point(i, j));
        visited[i][j] = -1;
        int maxVal = 1;

        while (!q.isEmpty()) {
            Point cur = q.poll();
            for (int[] d : dir) {
                int ny = cur.y + d[0];
                int nx = cur.x + d[1];
                if (ny < 0 || ny >= N || nx < 0 || nx >= M) continue;
                if (land[ny][nx] == 0 || visited[ny][nx] != 0) continue;
                q.add(new Point(ny, nx));
                visited[ny][nx] = -1;
                maxVal++;
            }
        }

        q.add(new Point(i, j));
        visited[i][j] = id;
        while (!q.isEmpty()) {
            Point cur = q.poll();
            for (int[] d : dir) {
                int ny = cur.y + d[0];
                int nx = cur.x + d[1];
                if (ny < 0 || ny >= N || nx < 0 || nx >= M) continue;
                if (visited[ny][nx] != -1) continue;
                q.add(new Point(ny, nx));
                visited[ny][nx] = id;
            }
        }
        size[id] = maxVal;
    }

    static class Point {
        int y, x;
        public Point(int y, int x) {
            this.y = y;
            this.x = x;
        }
    }
}
```
