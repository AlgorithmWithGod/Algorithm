```java
import java.io.*;
import java.util.*;

public class Main {

    static int N, M;
    static int[][] map;
    static boolean[][] visited;
    static int[] dr = {-1,-1,-1,0,0,1,1,1};
    static int[] dc = {-1,0,1,-1,1,-1,0,1};

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        map = new int[N][M];
        visited = new boolean[N][M];

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < M; j++) {
                map[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        int count = 0;

        for (int r = 0; r < N; r++) {
            for (int c = 0; c < M; c++) {
                if (!visited[r][c]) {
                    if (bfs(r, c)) {
                        count++;
                    }
                }
            }
        }

        System.out.println(count);
    }

    static boolean bfs(int sr, int sc) {
        Queue<int[]> q = new LinkedList<>();
        visited[sr][sc] = true;
        q.add(new int[]{sr, sc});

        int height = map[sr][sc];
        boolean isPeak = true;

        while (!q.isEmpty()) {
            int[] cur = q.poll();
            int r = cur[0];
            int c = cur[1];

            for (int d = 0; d < 8; d++) {
                int nr = r + dr[d];
                int nc = c + dc[d];

                if (nr < 0 || nc < 0 || nr >= N || nc >= M) continue;

                if (map[nr][nc] > height) {
                    isPeak = false;
                }

                if (map[nr][nc] == height && !visited[nr][nc]) {
                    visited[nr][nc] = true;
                    q.add(new int[]{nr, nc});
                }
            }
        }

        return isPeak;
    }
}
```
