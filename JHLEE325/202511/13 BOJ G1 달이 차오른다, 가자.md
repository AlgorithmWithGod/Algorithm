```java
import java.io.*;
import java.util.*;

public class Main {
    static int N, M;
    static char[][] map;
    static boolean[][][] visited;
    static int[] dy = {-1, 1, 0, 0};
    static int[] dx = {0, 0, -1, 1};

    static class State {
        int y, x, keybit, dist;
        State(int y, int x, int keybit, int dist) {
            this.y = y;
            this.x = x;
            this.keybit = keybit;
            this.dist = dist;
        }
    }

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        map = new char[N][M];
        visited = new boolean[1<<6][N][M];
        int starty = 0;
        int startx = 0;

        for (int i = 0; i < N; i++) {
            String line = br.readLine();
            for (int j = 0; j < M; j++) {
                map[i][j] = line.charAt(j);
                if (map[i][j] == '0') {
                    starty = i; startx = j;
                    map[i][j] = '.';
                }
            }
        }

        int ans = bfs(starty, startx);
        System.out.println(ans);
    }

    static int bfs(int y, int x) {
        Queue<State> q = new LinkedList<>();
        q.offer(new State(y, x, 0, 0));
        visited[0][y][x] = true;

        while (!q.isEmpty()) {
            State cur = q.poll();
            if (map[cur.y][cur.x] == '1') {
                return cur.dist;
            }

            for (int d = 0; d < 4; d++) {
                int ny = cur.y + dy[d];
                int nx = cur.x + dx[d];
                int nKey = cur.keybit;

                if (ny < 0 || nx < 0 || ny >= N || nx >= M) continue;
                char ch = map[ny][nx];

                if (ch == '#') continue;

                if (ch >= 'A' && ch <= 'F') {
                    int needed = 1 << (ch - 'A');
                    if ((nKey & needed) == 0) continue;
                }
                if (ch >= 'a' && ch <= 'f') {
                    nKey = nKey | (1 << (ch - 'a'));
                }

                if (!visited[nKey][ny][nx]) {
                    visited[nKey][ny][nx] = true;
                    q.offer(new State(ny, nx, nKey, cur.dist + 1));
                }
            }
        }

        return -1;
    }
}
```
