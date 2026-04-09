```java
import java.io.*;
import java.util.ArrayDeque;
import java.util.Queue;
import java.util.StringTokenizer;

public class BJ_4179_불 {

    private static final int[] dx = { -1, 1, 0, 0 };
    private static final int[] dy = { 0, 0, -1, 1 };

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int R, C;
    private static char[][]    matrix;
    private static Queue<Node> q;
    private static boolean[][] visited;

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
        R = Integer.parseInt(st.nextToken());
        C = Integer.parseInt(st.nextToken());

        matrix = new char[R][C];
        visited = new boolean[R][C];
        q = new ArrayDeque<>();
        for (int i = 0; i < R; i++) {
            String line = br.readLine();
            for (int j = 0; j < C; j++) {
                matrix[i][j] = line.charAt(j);
                if (matrix[i][j] == 'J') {
                    q.offer(new Node(i, j, 0));
                    visited[i][j] = true;
                }
            }
        }

        for (int i = 0; i < R; i++) {
            for (int j = 0; j < C; j++) {
                if (matrix[i][j] == 'F') {
                    q.offer(new Node(i, j, -1));
                }
            }
        }
    }

    private static void sol() throws IOException {
        while (!q.isEmpty()) {
            Node cur = q.poll();

            // 지훈이의 현위치까지 불이 번진 경우
            if (cur.cnt >= 0 && matrix[cur.x][cur.y] == 'F') continue;

            for (int d = 0; d < 4; d++) {
                int nx = cur.x + dx[d];
                int ny = cur.y + dy[d];

                // 지훈이만
                if (OOB(nx, ny) && cur.cnt >= 0) {
                    bw.write(cur.cnt + 1 + "");
                    return;
                }

                if (OOB(nx, ny) || matrix[nx][ny] == 'F' || matrix[nx][ny] == '#') {
                    continue;
                }

                // 지훈이 이동 가능 여부
                if (cur.cnt >= 0 && visited[nx][ny]) continue;

                if (matrix[cur.x][cur.y] == 'F') {
                    matrix[nx][ny] = 'F';
                    q.offer(new Node(nx, ny, -1));
                } else {
                    visited[nx][ny] = true;
                    q.offer(new Node(nx, ny, cur.cnt + 1));
                }
            }
        }
        bw.write("IMPOSSIBLE");
    }

    private static boolean OOB(int x, int y) {
        return x < 0 || R <= x || y < 0 || C <= y;
    }

}
```