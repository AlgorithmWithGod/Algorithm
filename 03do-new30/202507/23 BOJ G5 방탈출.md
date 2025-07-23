```java
import java.util.*;
import java.io.*;

public class Main {
    static int N, M;
    static int[][] arr;
    static int maxPath, password;
    static int[] dr = {0, 0, -1, 1};
    static int[] dc = {-1, 1, 0, 0};
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        arr = new int[N][M];
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < M; j++) {
                arr[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        maxPath = 0;
        password = 0;
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                if (arr[i][j] > 0) {
                    bfs(i, j);
                }
            }
        }
        System.out.println(password);
        br.close();
    }

    private static void bfs(int r, int c) {
        boolean[][] visited = new boolean[N][M];
        Deque<int[]> dq = new ArrayDeque<>();
        dq.offerLast(new int[] {r, c, 1});
        visited[r][c] = true;
        int start = arr[r][c];

        while (!dq.isEmpty()) {
            int[] rc = dq.pollFirst();
            r = rc[0];
            c = rc[1];
            int path = rc[2];

            boolean hasNextPath = false;
            for (int i = 0; i < 4; i++) {
                int nr = r + dr[i];
                int nc = c + dc[i];
                if (nr < 0 || nr >= N || nc < 0 || nc >= M) continue;
                if (visited[nr][nc]) continue;
                if (arr[nr][nc] == 0) continue;
                hasNextPath = true;
                visited[nr][nc] = true;
                dq.offerLast(new int[] {nr, nc, path + 1});
            }

            if (!hasNextPath) {
                if (path > maxPath) {
                    maxPath = path;
                    password = start + arr[r][c];
                } else if (path == maxPath) {
                    password = Math.max(password, start + arr[r][c]);
                }
            }
        }
    }
}

```
