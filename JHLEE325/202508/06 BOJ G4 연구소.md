```java
import java.io.*;
import java.util.*;

public class Main {

    static int n, m;
    static int[][] board;
    static int maxSafe = 0;
    static int[][] dir = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        st = new StringTokenizer(br.readLine());
        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());

        board = new int[n][m];
        List<Integer> empties = new ArrayList<>();
        List<Integer> viruses = new ArrayList<>();

        for (int r = 0; r < n; r++) {
            st = new StringTokenizer(br.readLine());
            for (int c = 0; c < m; c++) {
                board[r][c] = Integer.parseInt(st.nextToken());
                if (board[r][c] == 0) empties.add(r * m + c);
                else if (board[r][c] == 2) viruses.add(r * m + c);
            }
        }

        int E = empties.size();

        for (int i = 0; i < E; i++) {
            for (int j = i + 1; j < E; j++) {
                for (int k = j + 1; k < E; k++) {
                    int[][] tmp = copyBoard(board);

                    placeWall(tmp, empties.get(i));
                    placeWall(tmp, empties.get(j));
                    placeWall(tmp, empties.get(k));

                    spreadVirus(tmp, viruses);

                    int safe = countSafe(tmp);
                    if (safe > maxSafe) maxSafe = safe;
                }
            }
        }

        System.out.println(maxSafe);
    }

    static int[][] copyBoard(int[][] src) {
        int[][] dst = new int[n][m];
        for (int r = 0; r < n; r++) {
            System.arraycopy(src[r], 0, dst[r], 0, m);
        }
        return dst;
    }

    static void placeWall(int[][] g, int pos) {
        int r = pos / m, c = pos % m;
        g[r][c] = 1;
    }

    static void spreadVirus(int[][] g, List<Integer> viruses) {
        ArrayDeque<int[]> q = new ArrayDeque<>();
        for (int v : viruses) {
            int vr = v / m, vc = v % m;
            q.add(new int[]{vr, vc});
        }
        while (!q.isEmpty()) {
            int[] cur = q.poll();
            int y = cur[0], x = cur[1];
            for (int d = 0; d < 4; d++) {
                int dy = y + dir[d][0], dx = x + dir[d][1];
                if (dy < 0 || dy >= n || dx < 0 || dx >= m) continue;
                if (g[dy][dx] == 0) {
                    g[dy][dx] = 2;
                    q.add(new int[]{dy, dx});
                }
            }
        }
    }

    static int countSafe(int[][] g) {
        int cnt = 0;
        for (int r = 0; r < n; r++) {
            for (int c = 0; c < m; c++) {
                if (g[r][c] == 0) cnt++;
            }
        }
        return cnt;
    }
}

```
