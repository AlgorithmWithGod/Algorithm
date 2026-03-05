```
import java.io.*;

import java.util.ArrayDeque;
import java.util.Arrays;
import java.util.Queue;
import java.util.StringTokenizer;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int[] dx = {1, 0, -1, 0};
    private static final int[] dy = {0, 1, 0, -1};
    private static char[][] map;
    private static boolean[][][][][][][][] visited;
    private static int[] start;
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

        map = new char[N][M];
        visited = new boolean[N][M][2][2][2][2][2][2];
        start = new int[2];

        for (int i = 0; i < N; i++) {
            map[i] = br.readLine().toCharArray();
            for (int j = 0; j < M; j++) {
                if (map[i][j] == '0') {
                    start[0] = i;
                    start[1] = j;
                }
            }
        }
    }

    private static int BFS() {
        Queue<int[]> q = new ArrayDeque<>();
        int result = 0;
        visited[start[0]][start[1]][0][0][0][0][0][0] = true;
        // 0: x, 1: y, 2: count, 3: a, 4: b, 5: c, 6: d, 7: e, 8: f
        q.add(new int[]{start[0], start[1], 0, 0, 0, 0, 0, 0, 0});

        while (!q.isEmpty()) {
            int[] current = q.poll();

            for (int i = 0; i < 4; i++) {
                int nx = current[0] + dx[i];
                int ny = current[1] + dy[i];

                if (OOB(nx, ny) || map[nx][ny] == '#' || visited[nx][ny][current[3]][current[4]][current[5]][current[6]][current[7]][current[8]]) continue;
                if ((map[nx][ny] == 'A' && current[3] == 1) || (map[nx][ny] == 'B' && current[4] == 1) || (map[nx][ny] == 'C' && current[5] == 1)
                        || (map[nx][ny] == 'D' && current[6] == 1) || (map[nx][ny] == 'E' && current[7] == 1) || (map[nx][ny] == 'F' && current[8] == 1)) {
                    visited[nx][ny][current[3]][current[4]][current[5]][current[6]][current[7]][current[8]] = true;
                    q.add(new int[] {nx, ny, current[2]+1, current[3], current[4], current[5], current[6], current[7], current[8]});
                }
                if (map[nx][ny] == 'a') {
                    visited[nx][ny][1][current[4]][current[5]][current[6]][current[7]][current[8]] = true;
                    q.add(new int[] {nx, ny, current[2]+1, 1, current[4], current[5], current[6], current[7], current[8]});
                } else if (map[nx][ny] == 'b') {
                    visited[nx][ny][current[3]][1][current[5]][current[6]][current[7]][current[8]] = true;
                    q.add(new int[]{nx, ny, current[2] + 1, current[3], 1, current[5], current[6], current[7], current[8]});
                } else if (map[nx][ny] == 'c') {
                    visited[nx][ny][current[3]][current[4]][1][current[6]][current[7]][current[8]] = true;
                    q.add(new int[]{nx, ny, current[2] + 1, current[3], current[4], 1, current[6], current[7], current[8]});
                } else if (map[nx][ny] == 'd') {
                    visited[nx][ny][current[3]][current[4]][current[5]][1][current[7]][current[8]] = true;
                    q.add(new int[]{nx, ny, current[2] + 1, current[3], current[4], current[5], 1, current[7], current[8]});
                } else if (map[nx][ny] == 'e') {
                    visited[nx][ny][current[3]][current[4]][current[5]][current[6]][1][current[8]] = true;
                    q.add(new int[]{nx, ny, current[2] + 1, current[3], current[4], current[5], current[6], 1, current[8]});
                } else if (map[nx][ny] == 'f') {
                    visited[nx][ny][current[3]][current[4]][current[5]][current[6]][current[7]][1] = true;
                    q.add(new int[]{nx, ny, current[2] + 1, current[3], current[4], current[5], current[6], current[7], 1});
                }

                if (map[nx][ny] == '0' || map[nx][ny] == '.') {
                    visited[nx][ny][current[3]][current[4]][current[5]][current[6]][current[7]][current[8]] = true;
                    q.add(new int[] {nx, ny, current[2]+1, current[3], current[4], current[5], current[6], current[7], current[8]});
                }

                if (map[nx][ny] == '1') {
                    result = current[2]+1;
                    return result;
                }
            }
        }

        return -1;
    }

    private static boolean OOB(int nx, int ny) {
        return nx < 0 || nx > N-1 || ny < 0 || ny > M-1;
    }

}
```
