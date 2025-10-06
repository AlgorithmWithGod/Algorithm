```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static boolean[][] board, visited;
    private static int N, answer;

    public static void main(String[] args) throws IOException {
        init();

        DFS(0, 0, true);
        int blackMax = answer;
        answer = 0;

        visited = new boolean[N][N];
        DFS(0, 0, false);
        int whiteMax = answer;
        answer = blackMax + whiteMax;

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        answer = 0;

        board = new boolean[N][N];
        visited = new boolean[N][N];

        for (int i = 0; i < N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            for (int j = 0; j < N; j++) {
                if ("1".equals(st.nextToken())) board[i][j] = true;
            }
        }
    }

    private static void DFS(int index, int count, boolean isBlack) {
        answer = Math.max(answer, count);

        for (int i = index; i < N * N; i++) {
            int x = i / N;
            int y = i % N;

            if ((x + y) % 2 == (isBlack ? 0 : 1)) continue;

            if (board[x][y] && canPlace(x, y)) {
                visited[x][y] = true;
                DFS(i + 1, count + 1, isBlack);
                visited[x][y] = false;
            }
        }
    }

    private static boolean canPlace(int x, int y) {
        for (int i = 1; x+i < N && y+i < N; i++) {
            if (visited[x+i][y+i]) return false;
        }
        for (int i = 1; x+i < N && y-i >= 0; i++) {
            if (visited[x+i][y-i]) return false;
        }
        for (int i = 1; x-i >= 0 && y+i < N; i++) {
            if (visited[x-i][y+i]) return false;
        }
        for (int i = 1; x-i >= 0 && y-i >= 0; i++) {
            if (visited[x-i][y-i]) return false;
        }
        return true;
    }
}
```
