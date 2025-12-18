```java
import java.io.*;
import java.util.*;

public class Main {
    
    static class Point {
        int r, c;
        public Point(int r, int c) {
            this.r = r;
            this.c = c;
        }
    }
    
    static int N, M;
    static int[][] map;
    static boolean[][] visited;

    static int[] dr = {-1, 1, 0, 0};
    static int[] dc = {0, 0, -1, 1};

    public static void main(String[] args) throws IOException {
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

        int area = 0;

        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                if (map[i][j] == 0 && !visited[i][j]) {
                    bfs(i, j);
                    area++;
                }
            }
        }

        System.out.println(area);
    }

    static void bfs(int sr, int sc) {
        Queue<Point> queue = new LinkedList<>();
        queue.add(new Point(sr, sc));
        visited[sr][sc] = true;

        while (!queue.isEmpty()) {
            Point current = queue.poll();

            for (int i = 0; i < 4; i++) {
                int nr = (current.r + dr[i] + N) % N;
                int nc = (current.c + dc[i] + M) % M;

                if (!visited[nr][nc] && map[nr][nc] == 0) {
                    visited[nr][nc] = true;
                    queue.add(new Point(nr, nc));
                }
            }
        }
    }
}
```
