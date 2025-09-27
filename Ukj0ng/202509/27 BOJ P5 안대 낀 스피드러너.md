```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int[] dx = {1, 0, -1, 0};
    private static final int[] dy = {0, 1, 0, -1};
    // 0: 아래, 1: 오른쪽, 2: 위, 3: 왼쪽
    private static int[][] map;
    private static boolean[][][][][][] visited;
    private static int N;

    public static void main(String[] args) throws IOException {
        init();
        int answer = BFS();

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        map = new int[N][N];
        visited = new boolean[N][N][4][N][N][4];

        for (int i = 0; i < N; i++) {
            char[] input = br.readLine().toCharArray();
            for (int j = 0; j < N; j++) {
                if (input[j] == 'H') {
                    map[i][j] = 1;
                }
            }
        }
    }

    private static int BFS() {
        Queue<int[]> q = new ArrayDeque<>();
        int time = 0;
        visited[N-1][0][1][N-1][0][2] = true;
        q.add(new int[] {N-1, 0, 1, N-1, 0, 2, 0});

        while (!q.isEmpty()) {
            int[] current = q.poll();

            if (current[0] == 0 && current[1] == N-1 && current[3] == 0 && current[4] == N-1) {
                time = current[6];
                break;
            }

            int nx1, ny1, nx2, ny2;
            int dir1, dir2;

            if (current[0] == 0 && current[1] == N-1) {
                nx1 = current[0];
                ny1 = current[1];
            } else {
                nx1 = current[0] + dx[current[2]];
                ny1 = current[1] + dy[current[2]];
            }

            if (current[3] == 0 && current[4] == N-1) {
                nx2 = current[3];
                ny2 = current[4];
            } else {
                nx2 = current[3] + dx[current[5]];
                ny2 = current[4] + dy[current[5]];
            }

            if (OOB(nx1, ny1) || map[nx1][ny1] == 1) {
                nx1 = current[0];
                ny1 = current[1];
            }

            if (OOB(nx2, ny2) || map[nx2][ny2] == 1) {
                nx2 = current[3];
                ny2 = current[4];
            }

            if (!visited[nx1][ny1][current[2]][nx2][ny2][current[5]]) {
                visited[nx1][ny1][current[2]][nx2][ny2][current[5]] = true;
                q.add(new int[] {nx1, ny1, current[2], nx2, ny2, current[5], current[6]+1});
            }

            dir1 = (current[2]+1) % 4;
            dir2 = (current[5]+1) % 4;

            if (!visited[current[0]][current[1]][dir1][current[3]][current[4]][dir2]) {
                visited[current[0]][current[1]][dir1][current[3]][current[4]][dir2] = true;
                q.add(new int[] {current[0], current[1], dir1, current[3], current[4], dir2, current[6]+1});
            }

            dir1 = current[2]-1 < 0 ? 3 : current[2]-1;
            dir2 = current[5]-1 < 0 ? 3 : current[5]-1;

            if (!visited[current[0]][current[1]][dir1][current[3]][current[4]][dir2]) {
                visited[current[0]][current[1]][dir1][current[3]][current[4]][dir2] = true;
                q.add(new int[] {current[0], current[1], dir1, current[3], current[4], dir2, current[6]+1});
            }

        }

        return time;
    }

    private static boolean OOB(int nx, int ny) {
        return nx < 0 || nx > N-1 || ny < 0 || ny > N-1;
    }
}
```
