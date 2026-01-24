```java
import java.io.*;
import java.util.ArrayDeque;
import java.util.Arrays;
import java.util.Deque;
import java.util.StringTokenizer;

public class BJ_9376_탈옥 {

    private static final int   INF = 10001;
    private static final int[] dx  = { -1, 1, 0, 0 };
    private static final int[] dy  = { 0, 0, -1, 1 };

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final StringBuilder   sb = new StringBuilder();
    private static       StringTokenizer st;

    private static int H, W;
    private static int[][]     prisoners;
    private static int[][][]   dist;
    private static char[][]    matrix;
    private static Deque<Node> dq;

    private static class Node {
        int x;
        int y;
        int cnt;

        Node(int x, int y, int cnt) {
            this.x = x;
            this.y = y;
            this.cnt = cnt;
        }

    }

    public static void main(String[] args) throws IOException {
        int T = Integer.parseInt(br.readLine());

        while (T-- > 0) {
            init();
            sol();
        }

        bw.write(sb.toString());
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());
        H = Integer.parseInt(st.nextToken());
        W = Integer.parseInt(st.nextToken());

        prisoners = new int[2][2];
        int idx = 0;

        matrix = new char[H + 2][W + 2];
        dist = new int[3][H + 2][W + 2];

        for (int i = 0; i < H + 2; i++) {
            Arrays.fill(dist[0][i], INF);
            Arrays.fill(dist[1][i], INF);
            Arrays.fill(dist[2][i], INF);
            Arrays.fill(matrix[i], '.');
        }

        for (int i = 1; i <= H; i++) {
            String line = br.readLine();
            for (int j = 1; j <= W; j++) {
                matrix[i][j] = line.charAt(j - 1);

                if (matrix[i][j] == '$') {
                    prisoners[idx][0] = i;
                    prisoners[idx++][1] = j;
                    matrix[i][j] = '.';
                }
            }
        }

        dq = new ArrayDeque<>();
    }

    private static void sol() {
        bfs(0, 0, 0);
        bfs(1, prisoners[0][0], prisoners[0][1]);
        bfs(2, prisoners[1][0], prisoners[1][1]);

        int ans = INF;
        for (int i = 0; i < H + 2; i++) {
            for (int j = 0; j < W + 2; j++) {
                if (matrix[i][j] == '*') continue;

                int sum = dist[0][i][j] + dist[1][i][j] + dist[2][i][j];
                if (matrix[i][j] == '#') sum -= 2;

                ans = Math.min(ans, sum);
            }
        }

        sb.append(ans).append('\n');
    }

    private static void bfs(int id, int x, int y) {
        dq.clear();
        dq.offer(new Node(x, y, 0));
        dist[id][x][y] = 0;

        while (!dq.isEmpty()) {
            Node cur = dq.poll();

            if (dist[id][cur.x][cur.y] < cur.cnt) continue;

            for (int d = 0; d < 4; d++) {
                int nx = cur.x + dx[d];
                int ny = cur.y + dy[d];

                if (OOB(nx, ny) || matrix[nx][ny] == '*') continue;

                int newDist = matrix[nx][ny] == '#' ? cur.cnt + 1 : cur.cnt;

                if (newDist < dist[id][nx][ny]) {
                    dist[id][nx][ny] = newDist;

                    if (newDist == cur.cnt) {
                        dq.offerFirst(new Node(nx, ny, newDist));
                    } else {
                        dq.offerLast(new Node(nx, ny, newDist));
                    }
                }
            }
        }
    }

    private static boolean OOB(int x, int y) {
        return x < 0 || H + 2 <= x || y < 0 || W + 2 <= y;
    }

}
```
