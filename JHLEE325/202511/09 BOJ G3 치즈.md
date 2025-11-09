```java
import java.io.*;
import java.util.*;

public class Main {
    static int N, M;
    static int[][] map;
    static boolean[][] external;
    static int[] dy = { -1, 0, 1, 0 };
    static int[] dx = { 0, 1, 0, -1 };

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        map = new int[N][M];
        int cheeseCount = 0;
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < M; j++) {
                map[i][j] = Integer.parseInt(st.nextToken());
                if (map[i][j] == 1) cheeseCount++;
            }
        }

        int time = 0;
        while (cheeseCount > 0) {
            external = new boolean[N][M];
            markExternalAir();

            List<int[]> meltList = new ArrayList<>();
            for (int i = 0; i < N; i++) {
                for (int j = 0; j < M; j++) {
                    if (map[i][j] == 1) {
                        int contact = 0;
                        for (int d = 0; d < 4; d++) {
                            int ny = i + dy[d];
                            int nx = j + dx[d];
                            if (ny < 0 || nx < 0 || ny >= N || nx >= M) continue;
                            if (external[ny][nx] && map[ny][nx] == 0) {
                                contact++;
                            }
                        }
                        if (contact >= 2) {
                            meltList.add(new int[]{i, j});
                        }
                    }
                }
            }
            for (int[] pos : meltList) {
                int y = pos[0], x = pos[1];
                map[y][x] = 0;
                cheeseCount--;
            }

            time++;
        }

        System.out.println(time);
    }

    static void markExternalAir() {
        Queue<int[]> q = new LinkedList<>();
        boolean[][] visited = new boolean[N][M];
        q.offer(new int[]{0, 0});
        visited[0][0] = true;
        external[0][0] = true;

        while (!q.isEmpty()) {
            int[] cur = q.poll();
            int y = cur[0], x = cur[1];
            for (int d = 0; d < 4; d++) {
                int ny = y + dy[d];
                int nx = x + dx[d];
                if (ny < 0 || nx < 0 || ny >= N || nx >= M) continue;
                if (visited[ny][nx]) continue;
                if (map[ny][nx] == 1) {
                    continue;
                }
                visited[ny][nx] = true;
                external[ny][nx] = true;
                q.offer(new int[]{ny, nx});
            }
        }
    }
}
```
