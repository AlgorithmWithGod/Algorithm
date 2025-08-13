```java
import java.io.*;
import java.util.*;

public class Main {

    static class Node {
        int y, x, t, type;

        Node(int y, int x, int t, int type) {
            this.y = y;
            this.x = x;
            this.t = t;
            this.type = type;
        }
    }

    static int r, c;
    static char[][] map;
    static boolean[][][] visited;
    static final int[][] dir = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};

    static boolean inRange(int y, int x) {
        return 0 <= y && y < r && 0 <= x && x < c;
    }

    static boolean isEdge(int y, int x) {
        return y == 0 || y == r - 1 || x == 0 || x == c - 1;
    }

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        r = Integer.parseInt(st.nextToken());
        c = Integer.parseInt(st.nextToken());

        map = new char[r][c];
        visited = new boolean[r][c][2];
        ArrayDeque<Node> q = new ArrayDeque<>();

        int sy = -1, sx = -1;

        for (int y = 0; y < r; y++) {
            String line = br.readLine();
            for (int x = 0; x < c; x++) {
                char ch = line.charAt(x);
                map[y][x] = ch;
                if (ch == 'F') {
                    visited[y][x][1] = true;
                    q.add(new Node(y, x, 0, 1));
                } else if (ch == 'J') {
                    sy = y;
                    sx = x;
                }
            }
        }

        visited[sy][sx][0] = true;
        q.add(new Node(sy, sx, 0, 0));

        while (!q.isEmpty()) {
            Node cur = q.poll();

            if (cur.type == 0) {
                if (isEdge(cur.y, cur.x)) {
                    System.out.println(cur.t + 1);
                    return;
                }
            }

            for (int d = 0; d < 4; d++) {
                int dy = cur.y + dir[d][0];
                int dx = cur.x + dir[d][1];

                if (!inRange(dy, dx)) continue;
                if (map[dy][dx] == '#') continue;

                if (cur.type == 1) {
                    if (!visited[dy][dx][1]) {
                        visited[dy][dx][1] = true;
                        q.add(new Node(dy, dx, cur.t + 1, 1));
                    }
                } else {
                    if (!visited[dy][dx][0] && !visited[dy][dx][1]) {
                        visited[dy][dx][0] = true;
                        q.add(new Node(dy, dx, cur.t + 1, 0));
                    }

                }
            }
        }
        System.out.println("IMPOSSIBLE");
    }
}
```
