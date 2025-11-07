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

        dist = new int[N+1][M+1][2];
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
        PriorityQueue<int[]> pq = new PriorityQueue<>((o1, o2) -> Integer.compare(o1[2], o2[2]));
        int result = -1;
        dist[1][1][0] = 0;
        // x, y, dist, skill
        pq.add(new int[]{1, 1, 0, 0});

        while (!pq.isEmpty()) {
            int[] current = pq.poll();

            if (dist[current[0]][current[1]][current[3]] < current[2]) continue;

            if (current[0] == N && current[1] == M) {
                result = current[2];
                break;
            }

            for (int i = 0; i < 4; i++) {
                int nx = current[0] + dx[i];
                int ny = current[1] + dy[i];

                if (OOB(nx, ny) || map[nx][ny] == 1 || dist[nx][ny][current[3]] <= current[2]+1) continue;
                dist[nx][ny][current[3]] = current[2]+1;
                pq.add(new int[]{nx, ny, current[2]+1, current[3]});
            }

            if (current[3] == 0) {
                for (int i = 0; i < 4; i++) {
                    switch (i) {
                        case 0:
                            for (int j = current[0]; j <= N; j++) {
                                if (dist[j][current[1]][1] <= current[2]+(j-current[0])) continue;
                                dist[j][current[1]][1] = current[2]+(j-current[0]);
                                pq.add(new int[]{j, current[1], current[2]+(j-current[0]), 1});
                            }
                            break;
                        case 1:
                            for (int j = current[1]; j <= M; j++) {
                                if (dist[current[0]][j][1] <= current[2]+(j-current[1])) continue;
                                dist[current[0]][j][1] = current[2]+(j-current[1]);
                                pq.add(new int[]{current[0], j, current[2]+(j-current[1]), 1});
                            }
                            break;
                        case 2:
                            for (int j = current[0]; j >= 1; j--) {
                                if (dist[j][current[1]][1] <= current[2]+(current[0]-j)) continue;
                                dist[j][current[1]][1] = current[2]+(current[0]-j);
                                pq.add(new int[]{j, current[1], current[2]+(current[0]-j), 1});
                            }
                            break;
                        default:
                            for (int j = current[1]; j >= 1; j--) {
                                if (dist[current[0]][j][1] <= current[2]+(current[1]-j)) continue;
                                dist[current[0]][j][1] = current[2]+(current[1]-j);
                                pq.add(new int[]{current[0], j, current[2]+(current[1]-j), 1});
                            }
                    }
                }
            }
        }

        return result;
    }

    private static boolean OOB(int nx, int ny) {
        return nx < 1 || nx > N || ny < 1 || ny > M;
    }
}
```
