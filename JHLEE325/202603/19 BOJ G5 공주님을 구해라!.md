```java
import java.io.*;
import java.util.*;

public class Main {

    static int N, M, T;
    static int[][] map;
    static boolean[][] visited;
    static int[] dx = {-1, 1, 0, 0};
    static int[] dy = {0, 0, -1, 1};

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        T = Integer.parseInt(st.nextToken());

        map = new int[N][M];
        visited = new boolean[N][M];

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < M; j++) {
                map[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        int result = bfs();

        if (result == -1) System.out.println("Fail");
        else System.out.println(result);
    }

    static int bfs() {
        Queue<int[]> q = new LinkedList<>();
        q.add(new int[]{0, 0, 0});
        visited[0][0] = true;

        int findGram = Integer.MAX_VALUE;
        int res = Integer.MAX_VALUE;

        while (!q.isEmpty()) {
            int[] cur = q.poll();
            int x = cur[0];
            int y = cur[1];
            int time = cur[2];

            if (time > T) break;

            if (x == N - 1 && y == M - 1) {
                res = time;
                break;
            }

            for (int i = 0; i < 4; i++) {
                int nx = x + dx[i];
                int ny = y + dy[i];

                if (nx >= 0 && nx < N && ny >= 0 && ny < M && !visited[nx][ny]) {
                    if (map[nx][ny] == 2) {
                        visited[nx][ny] = true;
                        findGram = time + 1 + Math.abs(N - 1 - nx) + Math.abs(M - 1 - ny);
                    }
                    else if (map[nx][ny] == 0) {
                        visited[nx][ny] = true;
                        q.add(new int[]{nx, ny, time + 1});
                    }
                }
            }
        }

        int finalMin = Math.min(findGram, res);
        return (finalMin <= T) ? finalMin : -1;
    }
}
```
