```java
import java.io.*;
import java.util.*;

public class Main {
    static int n;
    static int[][] map;
    static int[][] dist;
    static int[] dx = {1, -1, 0, 0};
    static int[] dy = {0, 0, 1, -1};
    static final int INF = 987654321;

    static class Node {
        int x, y;
        Node(int x, int y) {
            this.x = x;
            this.y = y;
        }
    }

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        n = Integer.parseInt(br.readLine());
        map = new int[n][n];
        dist = new int[n][n];

        for (int i = 0; i < n; i++) {
            String line = br.readLine();
            for (int j = 0; j < n; j++) {
                map[i][j] = line.charAt(j) - '0';
                dist[i][j] = INF;
            }
        }

        bfs();
        System.out.println(dist[n - 1][n - 1]);
    }

    static void bfs() {
        Deque<Node> dq = new ArrayDeque<>();
        dist[0][0] = 0;
        dq.add(new Node(0, 0));

        while (!dq.isEmpty()) {
            Node cur = dq.pollFirst();
            int x = cur.x, y = cur.y;

            for (int dir = 0; dir < 4; dir++) {
                int nx = x + dx[dir];
                int ny = y + dy[dir];
                if (nx < 0 || ny < 0 || nx >= n || ny >= n) continue;

                int cost = (map[nx][ny] == 0 ? 1 : 0);
                if (dist[x][y] + cost < dist[nx][ny]) {
                    dist[nx][ny] = dist[x][y] + cost;
                    if (cost == 0) dq.addFirst(new Node(nx, ny));
                    else dq.addLast(new Node(nx, ny));
                }
            }
        }
    }
}

```
