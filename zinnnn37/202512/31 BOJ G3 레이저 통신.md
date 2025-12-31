```java
import java.awt.*;
import java.io.*;
import java.util.*;
import java.util.Queue;

public class BJ_6087_레이저_통신 {

    private static final int[] dx = { -1, 1, 0, 0 };
    private static final int[] dy = { 0, 0, -1, 1 };

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int W, H, ans;
    private static Point start, end;
    private static char[][]    matrix;
    private static int[][][]   visited;
    private static Queue<Node> pq;

    private static class Node implements Comparable<Node> {
        int x;
        int y;
        int dir;
        int cnt;

        public Node(int x, int y, int dir, int cnt) {
            this.x = x;
            this.y = y;
            this.dir = dir;
            this.cnt = cnt;
        }

        @Override
        public int compareTo(Node o) {
            return Integer.compare(this.cnt, o.cnt);
        }

    }

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());
        W = Integer.parseInt(st.nextToken());
        H = Integer.parseInt(st.nextToken());

        visited = new int[H][W][4];
        for (int i = 0; i < H; i++) {
            for (int j = 0; j < W; j++) {
                Arrays.fill(visited[i][j], Integer.MAX_VALUE);
            }
        }

        pq = new PriorityQueue<>();
        matrix = new char[H][W];
        for (int i = 0; i < H; i++) {
            String line = br.readLine();
            for (int j = 0; j < W; j++) {
                matrix[i][j] = line.charAt(j);

                if (matrix[i][j] == 'C') {
                    if (Objects.isNull(start)) {
                        start = new Point(i, j);
                        for (int d = 0; d < 4; d++) {
                            visited[i][j][d] = 0;
                            pq.offer(new Node(i, j, d, 0));
                        }
                    } else {
                        end = new Point(i, j);
                    }
                }
            }
        }
    }

    private static void sol() throws IOException {
        while (!pq.isEmpty()) {
            Node cur = pq.poll();

            if (cur.x == end.x && cur.y == end.y) {
                int ans = Integer.MAX_VALUE;
                for (int d = 0; d < 4; d++) {
                    ans = Math.min(ans, visited[end.x][end.y][d]);
                }
                bw.write(ans + "");
                break;
            }

            if (cur.cnt > visited[cur.x][cur.y][cur.dir]) continue;

            for (int d = 0; d < 4; d++) {
                if (d == (cur.dir ^ 1)) continue;

                int nx = cur.x + dx[d];
                int ny = cur.y + dy[d];

                if (OOB(nx, ny) || matrix[nx][ny] == '*') continue;

                int nCnt = cur.cnt + (d == cur.dir ? 0 : 1);

                if (visited[nx][ny][d] > nCnt) {
                    visited[nx][ny][d] = nCnt;
                    pq.offer(new Node(nx, ny, d, nCnt));
                }
            }
        }
        bw.flush();
        bw.close();
        br.close();
    }

    private static boolean OOB(int x, int y) {
        return x < 0 || H <= x || y < 0 || W <= y;
    }

}
```
