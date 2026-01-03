```java
import java.io.*;
import java.util.ArrayDeque;
import java.util.Arrays;
import java.util.Deque;
import java.util.StringTokenizer;

public class BJ_14497_주난의_난 {

    private static final int   INF = 987654321;
    private static final int[] dx  = { -1, 1, 0, 0 };
    private static final int[] dy  = { 0, 0, -1, 1 };

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int N, M;
    private static int[]       points;
    private static int[][]     dist;
    private static char[][]    matrix;
    private static Deque<Node> q;

    private static class Node {
        int x;
        int y;
        int cnt;

        public Node(int x, int y, int cnt) {
            this.x = x;
            this.y = y;
            this.cnt = cnt;
        }

    }

    public static void main(String[] args) throws IOException {
        init();
        sol();

        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        points = new int[4];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < 4; i++) {
            points[i] = Integer.parseInt(st.nextToken()) - 1;
        }

        dist = new int[N][M];
        for (int i = 0; i < N; i++) {
            Arrays.fill(dist[i], INF);
        }

        matrix = new char[N][M];
        for (int i = 0; i < N; i++) {
            String line = br.readLine();
            for (int j = 0; j < M; j++) {
                matrix[i][j] = line.charAt(j);
            }
        }
        q = new ArrayDeque<>();
    }

    private static void sol() throws IOException {
        q.offer(new Node(points[0], points[1], 0));
        dist[points[0]][points[1]] = 0;

        while (!q.isEmpty()) {
            Node cur = q.poll();

            if (dist[cur.x][cur.y] < cur.cnt) continue;

            if (matrix[cur.x][cur.y] == '#') {
                bw.write(cur.cnt + "");
                return;
            }

            for (int d = 0; d < 4; d++) {
                int nx = cur.x + dx[d];
                int ny = cur.y + dy[d];

                if (OOB(nx, ny)) continue;

                int newDist = cur.cnt + (matrix[nx][ny] == '0' ? 0 : 1);

                if (newDist < dist[nx][ny]) {
                    dist[nx][ny] = newDist;

                    if (matrix[nx][ny] == '0') {
                        q.offerFirst(new Node(nx, ny, newDist));
                    } else {
                        q.offerLast(new Node(nx, ny, newDist));
                    }
                }
            }
        }
    }

    private static boolean OOB(int x, int y) {
        return x < 0 || N <= x || y < 0 || M <= y;
    }

}
```
