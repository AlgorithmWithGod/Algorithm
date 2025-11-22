```java
import java.io.*;
import java.util.*;

public class Main {

    static int N;
    static char[][] map;
    static List<int[]> blank = new ArrayList<>();
    static List<int[]> teacher = new ArrayList<>();
    static boolean found = false; // 성공 여부

    static int[] dr = {-1, 1, 0, 0};
    static int[] dc = {0, 0, -1, 1};

    public static void main(String[] args) throws Exception {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());

        map = new char[N][N];

        for (int i = 0; i < N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            for (int j = 0; j < N; j++) {
                map[i][j] = st.nextToken().charAt(0);

                if (map[i][j] == 'X') blank.add(new int[]{i, j});
                if (map[i][j] == 'T') teacher.add(new int[]{i, j});
            }
        }

        dfs(0, 0);

        System.out.println(found ? "YES" : "NO");
    }

    static void dfs(int idx, int cnt) {
        if (found) return;

        if (cnt == 3) {
            if (check()) found = true;
            return;
        }

        if (idx >= blank.size()) return;

        int r = blank.get(idx)[0];
        int c = blank.get(idx)[1];

        map[r][c] = 'O';
        dfs(idx + 1, cnt + 1);

        map[r][c] = 'X';
        dfs(idx + 1, cnt);
    }

    static boolean check() {
        for (int[] t : teacher) {
            int tr = t[0];
            int tc = t[1];

            for (int d = 0; d < 4; d++) {
                int nr = tr;
                int nc = tc;

                while (true) {
                    nr += dr[d];
                    nc += dc[d];

                    if (nr < 0 || nc < 0 || nr >= N || nc >= N) break;

                    if (map[nr][nc] == 'O') break;
                    if (map[nr][nc] == 'S') return false;
                }
            }
        }
        return true;
    }
}
```
