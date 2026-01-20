```
import java.io.*;
import java.util.*;

public class Main {
    static int N, M;
    static int[][] board;
    static boolean[][] visited;
    static int maxScore = 0;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        board = new int[N][M];
        visited = new boolean[N][M];

        for (int i = 0; i < N; i++) {
            String line = br.readLine();
            for (int j = 0; j < M; j++) {
                board[i][j] = line.charAt(j) - '0';
            }
        }

        dfs(0, 0, 0);
        System.out.println(maxScore);
    }

    static void dfs(int r, int c, int sum) {
        if (r >= N) {
            maxScore = Math.max(maxScore, sum);
            return;
        }

        if (c >= M) {
            dfs(r + 1, 0, sum);
            return;
        }

        if (visited[r][c]) {
            dfs(r, c + 1, sum);
            return;
        }

        int current = 0;
        for (int len = 0; c + len < M; len++) {
            if (visited[r][c + len]) break;

            for (int i = 0; i <= len; i++) visited[r][c + i] = true;
            current = current * 10 + board[r][c + len];
            
            dfs(r, c + len + 1, sum + current);
            
            for (int i = 0; i <= len; i++) visited[r][c + i] = false;
        }

        current = board[r][c];
        for (int len = 1; r + len < N; len++) {
            if (visited[r + len][c]) break;

            for (int i = 1; i <= len; i++) visited[r + i][c] = true;
            
            int tempVal = 0;
            for (int i = 0; i <= len; i++) {
                tempVal = tempVal * 10 + board[r + i][c];
            }
            
            dfs(r, c + 1, sum + tempVal);
            
            for (int i = 1; i <= len; i++) visited[r + i][c] = false;
        }
    }
}
```
