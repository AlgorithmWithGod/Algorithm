```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.PriorityQueue;
import java.util.StringTokenizer;

import org.w3c.dom.Node;

public class Main {
    static final int MAX = 500;
    static final int INF = Integer.MAX_VALUE;
    static int[][] map = new int[MAX + 1][MAX + 1]; // 0: safe, 1: danger, 2: death
    static int[][] dist = new int[MAX + 1][MAX + 1];
    static int[] dr = {1, -1, 0, 0};
    static int[] dc = {0, 0, 1, -1};

    static class Node {
        int r, c, cost;
        Node(int r, int c, int cost) {
            this.r = r;
            this.c = c;
            this.cost = cost;
        }
    }
    public static void main(String[] args) throws IOException {
        var br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        int N = Integer.parseInt(br.readLine());
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            int x1 = Integer.parseInt(st.nextToken());
            int y1 = Integer.parseInt(st.nextToken());
            int x2 = Integer.parseInt(st.nextToken());
            int y2 = Integer.parseInt(st.nextToken());
            markArea(x1, y1, x2, y2, 1);
        }
        int M = Integer.parseInt(br.readLine());
        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int x1 = Integer.parseInt(st.nextToken());
            int y1 = Integer.parseInt(st.nextToken());
            int x2 = Integer.parseInt(st.nextToken());
            int y2 = Integer.parseInt(st.nextToken());
            markArea(x1, y1, x2, y2, 2);
        }

        for (int[] row : dist)
            Arrays.fill(row, INF);
        dist[0][0] = 0;
        PriorityQueue<Node> pq = new PriorityQueue<>((a, b) -> a.cost - b.cost);
        pq.add(new Node(0, 0, 0));
        while (!pq.isEmpty()) {
            Node cur = pq.poll();
            if (cur.cost > dist[cur.r][cur.c])
                continue;
            if (cur.r == MAX && cur.c == MAX)
                break;
            for (int d = 0; d < 4; d++) {
                int nr = cur.r + dr[d];
                int nc = cur.c + dc[d];
                if (nr < 0 || nr > MAX || nc < 0 || nc > MAX)
                    continue;
                if (map[nr][nc] == 2)
                    continue;
                int ncst = cur.cost + (map[nr][nc] == 1 ? 1 : 0);
                if (ncst < dist[nr][nc]) {
                    dist[nr][nc] = ncst;
                    pq.add(new Node(nr, nc, ncst));
                }
            }
        }
        int answer = dist[MAX][MAX];
        System.out.println(answer == INF ? -1 : answer);
    }

    static void markArea(int x1, int y1, int x2, int y2, int val) {
        int sx = Math.min(x1, x2);
        int ex = Math.max(x1, x2);
        int sy = Math.min(y1, y2);
        int ey = Math.max(y1, y2);
        for (int i = sx; i <= ex; i++) {
            for (int j = sy; j <= ey; j++) {
                map[i][j] = val;
            }
        }
    }

}

```
