```java
import java.util.*;
import java.io.*;

public class Main {
    static class State {
        int x1, y1, dir1;
        int x2, y2, dir2;
        int steps;

        State(int x1, int y1, int dir1, int x2, int y2, int dir2, int steps) {
            this.x1 = x1;
            this.y1 = y1;
            this.dir1 = dir1;
            this.x2 = x2;
            this.y2 = y2;
            this.dir2 = dir2;
            this.steps = steps;
        }
    }

    static int N;
    static char[][] map;
    static int[] dx = {-1, 0, 1, 0};
    static int[] dy = {0, 1, 0, -1};

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());
        map = new char[N][N];

        for (int i = 0; i < N; i++) {
            String line = br.readLine();
            for (int j = 0; j < N; j++) {
                map[i][j] = line.charAt(j);
            }
        }

        System.out.println(bfs());
    }

    public static int bfs() {
        Queue<State> q = new LinkedList<>();
        boolean[][][][][][] visited = new boolean[N][N][4][N][N][4];

        State start = new State(N-1, 0, 0, N-1, 0, 1, 0);
        q.offer(start);
        visited[N-1][0][0][N-1][0][1] = true;

        while (!q.isEmpty()) {
            State cur = q.poll();

            if (cur.x1 == 0 && cur.y1 == N-1 && cur.x2 == 0 && cur.y2 == N-1) {
                return cur.steps;
            }

            int nx1 = cur.x1;
            int ny1 = cur.y1;
            int nx2 = cur.x2;
            int ny2 = cur.y2;

            if (!(cur.x1 == 0 && cur.y1 == N-1)) {
                nx1 = cur.x1 + dx[cur.dir1];
                ny1 = cur.y1 + dy[cur.dir1];
                if (!isValid(nx1, ny1)) {
                    nx1 = cur.x1;
                    ny1 = cur.y1;
                }
            }

            if (!(cur.x2 == 0 && cur.y2 == N-1)) {
                nx2 = cur.x2 + dx[cur.dir2];
                ny2 = cur.y2 + dy[cur.dir2];
                if (!isValid(nx2, ny2)) {
                    nx2 = cur.x2;
                    ny2 = cur.y2;
                }
            }

            if (!visited[nx1][ny1][cur.dir1][nx2][ny2][cur.dir2]) {
                visited[nx1][ny1][cur.dir1][nx2][ny2][cur.dir2] = true;
                q.offer(new State(nx1, ny1, cur.dir1, nx2, ny2, cur.dir2, cur.steps + 1));
            }

            int newDir1 = (cur.dir1 + 3) % 4;
            int newDir2 = (cur.dir2 + 3) % 4;

            if (!visited[cur.x1][cur.y1][newDir1][cur.x2][cur.y2][newDir2]) {
                visited[cur.x1][cur.y1][newDir1][cur.x2][cur.y2][newDir2] = true;
                q.offer(new State(cur.x1, cur.y1, newDir1, cur.x2, cur.y2, newDir2, cur.steps + 1));
            }

            newDir1 = (cur.dir1 + 1) % 4;
            newDir2 = (cur.dir2 + 1) % 4;

            if (!visited[cur.x1][cur.y1][newDir1][cur.x2][cur.y2][newDir2]) {
                visited[cur.x1][cur.y1][newDir1][cur.x2][cur.y2][newDir2] = true;
                q.offer(new State(cur.x1, cur.y1, newDir1, cur.x2, cur.y2, newDir2, cur.steps + 1));
            }
        }

        return -1;
    }

    static boolean isValid(int x, int y) {
        return x >= 0 && x < N && y >= 0 && y < N && map[x][y] == 'E';
    }
}
```
