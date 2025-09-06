```java
import java.io.*;
import java.util.*;

public class Main {

    static class Point {
        int l, r, c, time;

        public Point(int l, int r, int c, int time) {
            this.l = l;
            this.r = r;
            this.c = c;
            this.time = time;
        }
    }

    static int l, r, c;
    static char[][][] building;
    static boolean[][][] visited;
    static int[] dl = {0, 0, 0, 0, -1, 1};
    static int[] dr = {0, 0, -1, 1, 0, 0};
    static int[] dc = {-1, 1, 0, 0, 0, 0};

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        while (true) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            l = Integer.parseInt(st.nextToken());
            r = Integer.parseInt(st.nextToken());
            c = Integer.parseInt(st.nextToken());

            if (l == 0 && r == 0 && c == 0) {
                break;
            }

            building = new char[l][r][c];
            visited = new boolean[l][r][c];
            Point start = null;

            for (int l = 0; l < Main.l; l++) {
                for (int r = 0; r < Main.r; r++) {
                    String line = br.readLine();
                    for (int c = 0; c < Main.c; c++) {
                        building[l][r][c] = line.charAt(c);
                        if (building[l][r][c] == 'S') {
                            start = new Point(l, r, c, 0);
                        }
                    }
                }
                br.readLine();
            }

            int result = bfs(start);

            if (result == -1) {
                sb.append("Trapped!\n");
            } else {
                sb.append("Escaped in ").append(result).append(" minute(s).\n");
            }
        }
        System.out.print(sb);
    }

    static int bfs(Point start) {
        Queue<Point> queue = new LinkedList<>();
        queue.offer(start);
        visited[start.l][start.r][start.c] = true;

        while (!queue.isEmpty()) {
            Point cur = queue.poll();

            if (building[cur.l][cur.r][cur.c] == 'E') {
                return cur.time;
            }

            for (int i = 0; i < 6; i++) {
                int nl = cur.l + dl[i];
                int nr = cur.r + dr[i];
                int nc = cur.c + dc[i];
                
                if (nl >= 0 && nl < l && nr >= 0 && nr < r && nc >= 0 && nc < c) {
                    if (!visited[nl][nr][nc] && building[nl][nr][nc] != '#') {
                        visited[nl][nr][nc] = true;
                        queue.offer(new Point(nl, nr, nc, cur.time + 1));
                    }
                }
            }
        }

        return -1;
    }
}
```
