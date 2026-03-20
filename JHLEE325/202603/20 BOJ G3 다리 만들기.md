```java
import java.io.*;
import java.util.*;

public class Main {
    
    static int N;
    static int[][] map;
    static boolean[][] visited;
    static int[] dx = {-1, 1, 0, 0};
    static int[] dy = {0, 0, -1, 1};
    static int minDist = Integer.MAX_VALUE;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());
        map = new int[N][N];
        visited = new boolean[N][N];

        for (int i = 0; i < N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            for (int j = 0; j < N; j++) {
                map[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        int islandIdx = 2;
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                if (map[i][j] == 1) {
                    numbering(i, j, islandIdx++);
                }
            }
        }

        for (int i = 2; i < islandIdx; i++) {
            bfs(i);
        }

        System.out.println(minDist);
    }

    static void numbering(int r, int c, int idx) {
        Deque<int[]> q = new ArrayDeque<>();
        q.add(new int[]{r, c});
        map[r][c] = idx;
        visited[r][c] = true;

        while (!q.isEmpty()) {
            int[] cur = q.poll();
            for (int i = 0; i < 4; i++) {
                int nx = cur[0] + dx[i];
                int ny = cur[1] + dy[i];
                if (nx >= 0 && nx < N && ny >= 0 && ny < N && !visited[nx][ny] && map[nx][ny] == 1) {
                    visited[nx][ny] = true;
                    map[nx][ny] = idx;
                    q.add(new int[]{nx, ny});
                }
            }
        }
    }

    static void bfs(int curIdx) {
        Deque<int[]> q = new ArrayDeque<>();
        boolean[][] check = new boolean[N][N];

        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                if (map[i][j] == curIdx) {
                    check[i][j] = true;
                    q.add(new int[]{i, j, 0});
                }
            }
        }

        while (!q.isEmpty()) {
            int[] cur = q.poll();
            int r = cur[0];
            int c = cur[1];
            int dist = cur[2];

            if (dist >= minDist) break;

            for (int i = 0; i < 4; i++) {
                int nx = r + dx[i];
                int ny = c + dy[i];

                if (nx >= 0 && nx < N && ny >= 0 && ny < N && !check[nx][ny]) {
                    if (map[nx][ny] == 0) {
                        check[nx][ny] = true;
                        q.add(new int[]{nx, ny, dist + 1});
                    } else if (map[nx][ny] != curIdx) {
                        minDist = Math.min(minDist, dist);
                        return;
                    }
                }
            }
        }
    }
}
```
