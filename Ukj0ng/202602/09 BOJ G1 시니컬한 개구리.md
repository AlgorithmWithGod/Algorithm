```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int[] dx = {1, 0, -1, 0};
    private static final int[] dy = {0, 1, 0, -1};
    private static int[][] map;
    private static int[][][] visited;
    private static boolean[] rowCheck;
    private static boolean[] colCheck;
    private static int[] start, end;
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

        map = new int[N+1][M+1];
        visited = new int[N+1][M+1][2];
        rowCheck = new boolean[N+1];
        colCheck = new boolean[M+1];

        st = new StringTokenizer(br.readLine());
        start = new int[2];
        end = new int[2];
        start[0] = Integer.parseInt(st.nextToken());
        start[1] = Integer.parseInt(st.nextToken());
        end[0] = Integer.parseInt(st.nextToken());
        end[1] = Integer.parseInt(st.nextToken());

        for (int i = 1; i <= N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 1; j <= M; j++) {
                map[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        for (int i = 1; i <= N; i++) {
            for (int j = 1; j <= M; j++) {
                Arrays.fill(visited[i][j], Integer.MAX_VALUE);
            }
        }
    }

    private static int BFS() {
        Queue<int[]> q = new ArrayDeque<>();
        int result = -1;
        visited[start[0]][start[1]][0] = 0;
        // x, y, 점프 횟수, 무시 유무
        q.add(new int[] {start[0], start[1], 0, 0});

        while (!q.isEmpty()) {
            int[] current = q.poll();
            if (current[0] == end[0] && current[1] == end[1]) {
                result = current[2];
                break;
            }

            for (int i = 0; i < 4; i++) {
                int nx = current[0] + dx[i] * map[current[0]][current[1]];
                int ny = current[1] + dy[i] * map[current[0]][current[1]];

                if (OOB(nx, ny)) continue;
                if (visited[nx][ny][current[3]] == Integer.MAX_VALUE) {
                    visited[nx][ny][current[3]] = current[2]+1;
                    q.add(new int[]{nx, ny, current[2]+1, current[3]});
                }
            }

            if (current[3] == 0){
                if (!rowCheck[current[0]]) {
                    rowCheck[current[0]] = true;
                    for (int j = 1; j <= M; j++) {
                        if (visited[current[0]][j][1] == Integer.MAX_VALUE) {
                            visited[current[0]][j][1] = current[2]+1;
                            q.add(new int[]{current[0], j, current[2]+1, 1});
                        }
                    }
                }

                if (!colCheck[current[1]]) {
                    colCheck[current[1]] = true;
                    for (int i = 1; i <= N; i++) {
                        if (visited[i][current[1]][1] == Integer.MAX_VALUE) {
                            visited[i][current[1]][1] = current[2]+1;
                            q.add(new int[]{i, current[1], current[2]+1, 1});
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
