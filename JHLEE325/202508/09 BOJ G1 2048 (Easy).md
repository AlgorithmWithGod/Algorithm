```java
import java.io.*;
import java.util.*;

public class Main {
    static int n;
    static int answer = 0;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        n = Integer.parseInt(br.readLine());
        StringTokenizer st;

        int[][] board = new int[n][n];

        for (int i = 0; i < n; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < n; j++) {
                board[i][j] = Integer.parseInt(st.nextToken());
                answer = Math.max(answer, board[i][j]);
            }
        }
        dfs(0, board);
        System.out.println(answer);
    }

    static void dfs(int depth, int[][] b) {
        if (depth == 5) {
            answer = Math.max(answer, maxTile(b));
            return;
        }
        dfs(depth + 1, moveUp(b));
        dfs(depth + 1, moveDown(b));
        dfs(depth + 1, moveLeft(b));
        dfs(depth + 1, moveRight(b));
    }

    static int maxTile(int[][] b) {
        int mx = 0;
        for (int[] row : b) for (int v : row) mx = Math.max(mx, v);
        return mx;
    }

    static int[][] moveLeft(int[][] b) {
        int[][] nb = new int[n][n];
        for (int r = 0; r < n; r++) {
            Deque<Integer> q = new ArrayDeque<>();
            for (int c = 0; c < n; c++) if (b[r][c] != 0) q.offerLast(b[r][c]);

            int idx = 0;
            while (!q.isEmpty()) {
                int cur = q.pollFirst();
                if (!q.isEmpty() && cur == q.peekFirst()) {
                    cur += q.pollFirst();
                }
                nb[r][idx++] = cur;
                answer = Math.max(answer, cur);
            }
        }
        return nb;
    }

    static int[][] moveRight(int[][] b) {
        int[][] nb = new int[n][n];
        for (int r = 0; r < n; r++) {
            Deque<Integer> q = new ArrayDeque<>();
            for (int c = n - 1; c >= 0; c--) if (b[r][c] != 0) q.offerLast(b[r][c]);

            int idx = n - 1;
            while (!q.isEmpty()) {
                int cur = q.pollFirst();
                if (!q.isEmpty() && cur == q.peekFirst()) {
                    cur += q.pollFirst();
                }
                nb[r][idx--] = cur;
                answer = Math.max(answer, cur);
            }
        }
        return nb;
    }

    static int[][] moveUp(int[][] b) {
        int[][] nb = new int[n][n];
        for (int c = 0; c < n; c++) {
            Deque<Integer> q = new ArrayDeque<>();
            for (int r = 0; r < n; r++) if (b[r][c] != 0) q.offerLast(b[r][c]);

            int idx = 0;
            while (!q.isEmpty()) {
                int cur = q.pollFirst();
                if (!q.isEmpty() && cur == q.peekFirst()) {
                    cur += q.pollFirst();
                }
                nb[idx++][c] = cur;
                answer = Math.max(answer, cur);
            }
        }
        return nb;
    }

    static int[][] moveDown(int[][] b) {
        int[][] nb = new int[n][n];
        for (int c = 0; c < n; c++) {
            Deque<Integer> q = new ArrayDeque<>();
            for (int r = n - 1; r >= 0; r--) if (b[r][c] != 0) q.offerLast(b[r][c]);

            int idx = n - 1;
            while (!q.isEmpty()) {
                int cur = q.pollFirst();
                if (!q.isEmpty() && cur == q.peekFirst()) {
                    cur += q.pollFirst();
                }
                nb[idx--][c] = cur;
                answer = Math.max(answer, cur);
            }
        }
        return nb;
    }
}

```
