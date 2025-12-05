```java
import java.awt.*;
import java.io.*;
import java.util.ArrayDeque;
import java.util.Queue;
import java.util.StringTokenizer;

public class BJ_19606_Escape_Room {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int M, N;
    private static int[][]      matrix;
    private static boolean[]    checked;
    private static boolean[][]  visited;
    private static Queue<Point> q;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        M = Integer.parseInt(br.readLine());
        N = Integer.parseInt(br.readLine());

        checked = new boolean[1_000_001];
        matrix = new int[M + 1][N + 1];
        for (int i = 1; i <= M; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 1; j <= N; j++) {
                matrix[i][j] = Integer.parseInt(st.nextToken());
            }
        }
        visited = new boolean[M + 1][N + 1];
        q = new ArrayDeque<>();
    }

    private static void sol() throws IOException {
        bfs();
        bw.flush();
        bw.close();
        br.close();
    }

    private static void bfs() throws IOException {
        q.offer(new Point(1, 1));
        visited[1][1] = true;

        while (!q.isEmpty()) {
            Point cur = q.poll();

            if (cur.x == M && cur.y == N) {
                bw.write("yes");
                return;
            }

            int target = matrix[cur.x][cur.y];
            if (checked[target]) continue;
            checked[target] = true;

            for (int i = 1; i * i <= target; i++) {
                if (target % i != 0) continue;

                int nx = i;
                int ny = target / i;

                if (!OOB(nx, ny) && !visited[nx][ny]) {
                    q.offer(new Point(nx, ny));
                    visited[nx][ny] = true;
                }
                if (!OOB(ny, nx) && !visited[ny][nx]) {
                    q.offer(new Point(ny, nx));
                    visited[ny][nx] = true;
                }
            }
        }
        bw.write("no");
    }

    private static boolean OOB(int x, int y) {
        return x < 1 || x > M || y < 1 || y > N;
    }

}
```