```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int INF = (int) 1e9;
    private static final int[] dx = {1, 0, -1, 0};
    private static final int[] dy = {0, 1, 0, -1};
    private static int[][][] dist;
    private static int[][] map;
    private static int N, M;
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

        dist = new int[N+1][M+1][6];
        map = new int[N+1][M+1];

        for (int i = 1; i <= N; i++) {
            char[] input = br.readLine().toCharArray();
            for (int j = 1; j <= M; j++) {
                map[i][j] = input[j-1] - '0';
                Arrays.fill(dist[i][j], INF);
            }
        }
    }

    private static int BFS() {
        Deque<int[]> q = new ArrayDeque<>();
        int result = INF;
        dist[1][1][0] = 0;
        // x, y, mode
        q.add(new int[]{1, 1, 0});

        while (!q.isEmpty()) {
            int[] current = q.poll();

            if (current[2] == 0) {
                for (int i = 0; i < 4; i++) {
                    int nx = current[0] + dx[i];
                    int ny = current[1] + dy[i];

                    if (OOB(nx, ny) || map[nx][ny] == 1 || dist[nx][ny][current[2]] <= dist[current[0]][current[1]][current[2]] + 1) continue;
                    dist[nx][ny][current[2]] = dist[current[0]][current[1]][current[2]] + 1;
                    q.addLast(new int[]{nx, ny, current[2]});
                }

                for (int i = 0; i < 4; i++) {
                    int newMode = i+2;
                    if (dist[current[0]][current[1]][current[2]] < dist[current[0]][current[1]][newMode]) {
                        dist[current[0]][current[1]][newMode] = dist[current[0]][current[1]][current[2]];
                        q.addFirst(new int[]{current[0], current[1], newMode});
                    }
                }
            } else if (current[2] == 1) {
                for (int i = 0; i < 4; i++) {
                    int nx = current[0] + dx[i];
                    int ny = current[1] + dy[i];

                    if (OOB(nx, ny) || map[nx][ny] == 1 || dist[nx][ny][current[2]] <= dist[current[0]][current[1]][current[2]] + 1) continue;
                    dist[nx][ny][current[2]] = dist[current[0]][current[1]][current[2]] + 1;
                    q.addLast(new int[]{nx, ny, current[2]});
                }
            } else {
                if (dist[current[0]][current[1]][current[2]] < dist[current[0]][current[1]][1]) {
                    dist[current[0]][current[1]][1] = dist[current[0]][current[1]][current[2]];
                    q.addFirst(new int[]{current[0], current[1], 1});
                }

                int dir = current[2]-2;
                int nx = current[0] + dx[dir];
                int ny = current[1] + dy[dir];

                if (OOB(nx, ny) || dist[nx][ny][current[2]] <= dist[current[0]][current[1]][current[2]] + 1) continue;
                dist[nx][ny][current[2]] = dist[current[0]][current[1]][current[2]] + 1;
                q.addLast(new int[]{nx, ny, current[2]});
            }
        }

        for (int i = 0; i < 6; i++) {
            result = Math.min(result, dist[N][M][i]);
        }

        return (result == INF) ? -1 : result;
    }

    private static boolean OOB(int nx, int ny) {
        return nx < 1 || nx > N || ny < 1 || ny > M;
    }
}
```
