```java
import java.io.*;
import java.util.*;

public class Main {

    static int N, M;
    static int[][] map;
    static int res = 0;
    static int[] dy = {-1, 1, 0, 0};
    static int[] dx = {0, 0, -1, 1};

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        map = new int[N][M];

        for (int i = 0; i < N; i++) {
            String s = br.readLine();
            for (int j = 0; j < M; j++) {
                char c = s.charAt(j);
                switch (c) {
                    case 'W': {
                        map[i][j] = 0;
                        break;
                    }
                    case 'L': {
                        map[i][j] = 1;
                        break;
                    }
                }
            }
        }

        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                if (map[i][j] == 1) {
                    bfs(i, j);
                }
            }
        }

        System.out.println(res);
    }

    static void bfs(int y, int x) {
        boolean[][] visited = new boolean[N][M];
        Queue<int[]> q = new ArrayDeque<>();
        visited[y][x] = true;
        q.add(new int[]{y, x});
        int temp = 0;

        while (!q.isEmpty()) {
            temp++;
            int s = q.size();
            for (int i = 0; i < s; i++) {
                int[] cur = q.poll();
                for (int d = 0; d < 4; d++) {
                    int ny = cur[0] + dy[d];
                    int nx = cur[1] + dx[d];
                    if (ny < 0 || nx < 0 || ny >= N || nx >= M || visited[ny][nx] || map[ny][nx] == 0)
                        continue;
                    visited[ny][nx] = true;
                    q.add(new int[]{ny, nx});
                }
            }
        }
        res = Math.max(res, temp - 1);
    }
}
```
