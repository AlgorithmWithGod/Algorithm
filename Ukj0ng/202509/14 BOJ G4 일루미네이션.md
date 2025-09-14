```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

    private static final int[] dx_even = {-1, -1, 0, 0, 1, 1};
    private static final int[] dy_even = {-1, 0, -1, 1, -1, 0};

    private static final int[] dx_odd = {-1, -1, 0, 0, 1, 1};
    private static final int[] dy_odd = {0, 1, -1, 1, 0, 1};

    private static int[][] board;
    private static int W, H, answer;

    public static void main(String[] args) throws IOException {
        init();

        markOutside();

        for (int i = 1; i <= H; i++) {
            for (int j = 1; j <= W; j++) {
                if (board[i][j] == 0) {
                    board[i][j] = 1;
                }
            }
        }

        for (int i = 1; i <= H; i++) {
            for (int j = 1; j <= W; j++) {
                if (board[i][j] == 1) {
                    answer += countWalls(i, j);
                }
            }
        }

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        W = Integer.parseInt(st.nextToken());
        H = Integer.parseInt(st.nextToken());

        board = new int[H+2][W+2];

        for (int i = 1; i <= H; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 1; j <= W; j++) {
                board[i][j] = Integer.parseInt(st.nextToken());
            }
        }
    }

    private static void markOutside() {
        Queue<int[]> q = new ArrayDeque<>();
        board[0][0] = -1;
        q.add(new int[]{0, 0});

        while (!q.isEmpty()) {
            int[] current = q.poll();
            int x = current[0];
            int y = current[1];

            int[] dx = (x % 2 == 0) ? dx_even : dx_odd;
            int[] dy = (x % 2 == 0) ? dy_even : dy_odd;

            for (int i = 0; i < 6; i++) {
                int nx = x + dx[i];
                int ny = y + dy[i];

                if (nx < 0 || nx >= H+2 || ny < 0 || ny >= W+2) continue;
                if (board[nx][ny] != 0) continue;

                board[nx][ny] = -1;
                q.add(new int[]{nx, ny});
            }
        }
    }

    private static int countWalls(int x, int y) {
        int walls = 0;

        int[] dx = (x % 2 == 0) ? dx_even : dx_odd;
        int[] dy = (x % 2 == 0) ? dy_even : dy_odd;

        for (int i = 0; i < 6; i++) {
            int nx = x + dx[i];
            int ny = y + dy[i];

            if (nx < 0 || nx >= H+2 || ny < 0 || ny >= W+2 || board[nx][ny] == -1) {
                walls++;
            }
        }

        return walls;
    }
}
```
