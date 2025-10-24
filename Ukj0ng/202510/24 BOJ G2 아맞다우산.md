```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int[] dx = {1, 0, -1, 0};
    private static final int[] dy = {0, 1, 0, -1};
    private static char[][] map;
    private static boolean[][][] visited;
    private static int[] start, end;
    private static int N, M, count;
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

        map = new char[M][N];
        start = new int[2];
        end = new int[2];

        for (int i = 0; i < M; i++) {
            map[i] = br.readLine().toCharArray();
            for (int j = 0; j < N; j++) {
                if (map[i][j] == 'S') {
                    start[0] = i;
                    start[1] = j;
                } else if (map[i][j] == 'E') {
                    end[0] = i;
                    end[1] = j;
                } else if (map[i][j] == 'X') {
                    map[i][j] = (char) (count + '0');
                    count++;
                }
            }
        }

        visited = new boolean[M][N][1 << count];
    }

    private static int BFS() {
        Queue<int[]> q = new ArrayDeque<>();
        int result = 0;
        visited[start[0]][start[1]][0] = true;
        q.add(new int[]{start[0], start[1], 0, 0});

        while (!q.isEmpty()) {
            int[] current = q.poll();

            if (current[0] == end[0] && current[1] == end[1] && current[2] == (1 << count)-1) {
                result = current[3];
                break;
            }

            for (int i = 0; i < 4; i++) {
                int nx = current[0] + dx[i];
                int ny = current[1] + dy[i];

                if (OOB(nx, ny) || map[nx][ny] == '#') continue;

                if (!isThings(nx, ny) && !visited[nx][ny][current[2]]) {
                    visited[nx][ny][current[2]] = true;
                    q.add(new int[]{nx, ny, current[2], current[3]+1});
                } else if (isThings(nx, ny)) {
                    int v = 1 << (map[nx][ny] - '0');
                    if (visited[nx][ny][current[2] | v]) continue;
                    visited[nx][ny][current[2] | v] = true;
                    q.add(new int[]{nx, ny, current[2] | v, current[3] + 1});
                }

            }
        }

        return result;
    }

    private static boolean OOB(int nx, int ny) {
        return nx < 0 || nx > M-1 || ny < 0 || ny > N-1;
    }

    private static boolean isThings(int nx, int ny) {
        return map[nx][ny] != '#' &&
                map[nx][ny] != 'S' &&
                map[nx][ny] != 'E' &&
                map[nx][ny] != '.';
    }
}
```
