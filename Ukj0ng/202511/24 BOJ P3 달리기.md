```
import java.io.*;
import java.util.ArrayDeque;
import java.util.Queue;
import java.util.StringTokenizer;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int[] dx = {1, 0, -1, 0};
    private static final int[] dy = {0, 1, 0, -1};
    private static char[][] map;
    private static int[][] dist, count;
    private static int[] start, end;
    private static int N, M, K;

    public static void main(String[] args) throws IOException {
        init();
        int answer = BFS();

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());

        map = new char[N + 1][M + 1];
        dist = new int[N + 1][M + 1];
        count = new int[N + 1][M + 1];

        start = new int[2];
        end = new int[2];

        for (int i = 1; i <= N; i++) {
            char[] input = br.readLine().toCharArray();
            for (int j = 1; j <= M; j++) {
                map[i][j] = input[j - 1];
                dist[i][j] = Integer.MAX_VALUE;
            }
        }

        st = new StringTokenizer(br.readLine());
        start[0] = Integer.parseInt(st.nextToken());
        start[1] = Integer.parseInt(st.nextToken());
        end[0] = Integer.parseInt(st.nextToken());
        end[1] = Integer.parseInt(st.nextToken());
    }

    private static int BFS() {
        Queue<int[]> q = new ArrayDeque<>();
        dist[start[0]][start[1]] = 0;
        q.add(new int[]{start[0], start[1], 0});

        while (!q.isEmpty()) {
            int[] current = q.poll();

            for (int i = 0; i < 4; i++) {
                int nx = current[0];
                int ny = current[1];
                if (i % 2 == 0) {
                    int k = 1;
                    while (k <= K && !OOB(nx + dx[i] * k, ny) && map[nx + dx[i] * k][ny] == '.') {
                        if (dist[nx + dx[i] * k][ny] < current[2] + 1) break;
                        dist[nx + dx[i] * k][ny] = Math.min(dist[nx + dx[i] * k][ny], current[2] + 1);
                        count[nx + dx[i] * k][ny]++;
                        if (count[nx + dx[i] * k][ny] <= 2) q.add(new int[]{nx + dx[i] * k, ny, current[2] + 1});
                        k++;
                    }
                } else {
                    int k = 1;
                    while (k <= K && !OOB(nx, ny + dy[i] * k) && map[nx][ny + dy[i] * k] == '.') {
                        if (dist[nx][ny + dy[i] * k] < current[2] + 1) break;
                        dist[nx][ny + dy[i] * k] = Math.min(dist[nx][ny + dy[i] * k], current[2] + 1);
                        count[nx][ny + dy[i] * k]++;
                        if (count[nx][ny + dy[i] * k] <= 2) q.add(new int[]{nx, ny + dy[i] * k, current[2] + 1});
                        k++;
                    }
                }
            }
        }

        return dist[end[0]][end[1]] != Integer.MAX_VALUE ? dist[end[0]][end[1]] : -1;
    }

    private static boolean OOB(int nx, int ny) {
        return nx < 1 || nx > N || ny < 1 || ny > M;
    }
}
```
