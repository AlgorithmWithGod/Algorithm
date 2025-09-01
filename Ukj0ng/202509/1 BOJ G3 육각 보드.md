```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int[] dx = {1, 1, 0, 0, -1, -1};
    private static final int[] dy = {0, -1, 1, -1, 0, 1};
    private static char[][] board;
    private static int[][] arr;
    private static int N, color;

    public static void main(String[] args) throws IOException {
        init();
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                if (board[i][j] == 'X' && arr[i][j] == 0) {
                    color = Math.max(color, 1);
                    BFS(i, j);
                }
            }
        }

        bw.write(color + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        color = 0;
        board = new char[N][N];
        arr = new int[N][N];

        for (int i = 0; i < N; i++) {
            board[i] = br.readLine().toCharArray();
        }
    }

    private static void BFS(int x, int y) {
        Queue<int[]> q = new ArrayDeque<>();
        arr[x][y] = 1;
        q.add(new int[]{x, y});

        while (!q.isEmpty()) {
            int[] current = q.poll();

            for (int i = 0; i < 6; i++) {
                int nx =  current[0] + dx[i];
                int ny = current[1] + dy[i];

                if (OOB(nx, ny) || board[nx][ny] != 'X') continue;
                if (arr[nx][ny] == 0) {
                    color = Math.max(color, 2);
                    arr[nx][ny] = 3 - arr[current[0]][current[1]];
                    q.add(new int[]{nx, ny});
                } else if (arr[nx][ny] == arr[current[0]][current[1]]) {
                    color = Math.max(color, 3);
                    return;
                }
            }
        }
    }

    private static boolean OOB(int nx, int ny) {
        return nx < 0 || nx > N-1 || ny < 0 || ny > N-1;
    }
}
```
