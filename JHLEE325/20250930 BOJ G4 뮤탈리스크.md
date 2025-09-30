```java
import java.io.*;
import java.util.*;

public class Main {
    static class State {
        int a, b, c, cnt;
        State(int a, int b, int c, int cnt) {
            this.a = a;
            this.b = b;
            this.c = c;
            this.cnt = cnt;
        }
    }

    static int[] dmg = {9, 3, 1};
    static boolean[][][] visited = new boolean[61][61][61];

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());

        int[] scv = new int[3];
        StringTokenizer st = new StringTokenizer(br.readLine());
        for (int i = 0; i < n; i++) {
            scv[i] = Integer.parseInt(st.nextToken());
        }

        System.out.println(bfs(scv[0], scv[1], scv[2]));
    }

    static int bfs(int a, int b, int c) {
        Queue<State> q = new LinkedList<>();
        q.add(new State(a, b, c, 0));
        visited[a][b][c] = true;

        while (!q.isEmpty()) {
            State cur = q.poll();
            int x = cur.a;
            int y = cur.b;
            int z = cur.c;

            if (x == 0 && y == 0 && z == 0) {
                return cur.cnt;
            }

            int[][] orders = {
                    {0,1,2}, {0,2,1},
                    {1,0,2}, {1,2,0},
                    {2,0,1}, {2,1,0}
            };

            for (int[] ord : orders) {
                int nx = Math.max(0, x - dmg[ord[0]]);
                int ny = Math.max(0, y - dmg[ord[1]]);
                int nz = Math.max(0, z - dmg[ord[2]]);

                if (!visited[nx][ny][nz]) {
                    visited[nx][ny][nz] = true;
                    q.add(new State(nx, ny, nz, cur.cnt + 1));
                }
            }
        }
        return -1;
    }
}
```
