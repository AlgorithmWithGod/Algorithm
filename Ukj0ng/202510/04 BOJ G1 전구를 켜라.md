```
import java.io.*;
import java.util.ArrayDeque;
import java.util.Arrays;
import java.util.Deque;
import java.util.StringTokenizer;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int[] dx = {1, 1, -1, -1};
    private static final int[] dy = {1, -1, 1, -1};
    private static final char[] need = {'\\', '/', '/', '\\'};
    private static int[][] dist;
    private static char[][] map;
    private static int N, M;

    public static void main(String[] args) throws IOException {
        init();

        int answer = BFS();

        if (answer == -1) {
            bw.write("NO SOLUTION");
        } else {
            bw.write(answer + "");
        }
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        map = new char[N][M];
        dist = new int[N+1][M+1];

        for (int i = 0; i < N; i++) {
            map[i] = br.readLine().toCharArray();
        }

        for (int i = 0; i <= N; i++) {
            Arrays.fill(dist[i], Integer.MAX_VALUE);
        }
    }

    private static int BFS() {
        Deque<int[]> dq = new ArrayDeque<>();
        dist[0][0] = 0;
        dq.add(new int[]{0, 0, 0});

        while (!dq.isEmpty()) {
            int[] current = dq.poll();

            if (dist[current[0]][current[1]] < current[2]) continue;

            for (int i = 0; i < 4; i++) {
                int nx = current[0] + dx[i];
                int ny = current[1] + dy[i];

                if (OOBPoint(nx, ny)) continue;

                int gx = Math.min(current[0], nx);
                int gy = Math.min(current[1], ny);

                if (OOBRange(gx, gy)) continue;

                int cost = (map[gx][gy] == need[i]) ? 0 : 1;
                int newDist = dist[current[0]][current[1]] + cost;

                if (newDist < dist[nx][ny]) {
                    dist[nx][ny] = newDist;

                    if (cost == 0) {
                        dq.addFirst(new int[]{nx, ny, newDist});
                    } else {
                        dq.addLast(new int[]{nx, ny, newDist});
                    }
                }
            }
        }

        return dist[N][M] == Integer.MAX_VALUE ? -1 : dist[N][M];
    }

    private static boolean OOBPoint(int nx, int ny) {
        return nx < 0 || nx > N || ny < 0 || ny > M;
    }

    private static boolean OOBRange(int gx, int gy) {
        return gx < 0 || gx >= N || gy < 0 || gy >= M;
    }
}
```
