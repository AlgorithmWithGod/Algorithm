```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int[] dx = {1, 0, -1, 0};
    private static final int[] dy = {0, 1, 0, -1};
    private static int[][] map;
    private static boolean[][][][] visited;
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

        map = new int[N][M];
        visited = new boolean[N][M][4][4];
        start = new int[2];

        int count = 1;
        for (int i = 0; i < N; i++) {
            char[] input = br.readLine().toCharArray();
            for (int j = 0; j < M; j++) {
                if (input[j] == 'S') {
                    start[0] = i;
                    start[1] = j;
                } else if (input[j] == '#') {
                    map[i][j] = -1;
                } else if (input[j] == 'C') {
                    map[i][j] = count++;
                }
            }
        }
    }

    private static int BFS() {
        Queue<int[]> q = new ArrayDeque<>();
        int result = -1;
        for (int i = 0; i < 4; i++) {
            visited[start[0]][start[1]][0][i] = true;
            q.add(new int[]{start[0], start[1], 0, i, 0});
        }

        while (!q.isEmpty()) {
            // x, y, C의 개수, 방향, 시간
            int[] current = q.poll();

            if (current[2] == 3) {
                result = current[4];
                break;
            }

            for (int i = 0; i < 4; i++) {
                if (current[3] == i) continue;
                int nx = current[0] + dx[i];
                int ny = current[1] + dy[i];

                if (OOB(nx, ny) || map[nx][ny] == -1) continue;
                int nCount = current[2] | map[nx][ny];

                if (nCount > 3 || visited[nx][ny][nCount][i]) continue;
                visited[nx][ny][nCount][i] = true;
                q.add(new int[]{nx, ny, nCount, i, current[4]+1});
            }
        }

        return result;
    }

    private static boolean OOB(int nx, int ny) {
        return nx < 0 || nx > N-1 || ny < 0 || ny > M-1;
    }
}
```
