```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.*;

public class Main {

    static int n, m;
    static int[][] map, meltcount;
    static boolean[][] visited;
    static int[][] dir = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());

        map = new int[n][m];
        visited = new boolean[n][m];

        for (int i = 0; i < n; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < m; j++) {
                int num = Integer.parseInt(st.nextToken());
                map[i][j] = num;
            }
        }

        int year = 0;
        while (true) {
            int count = countice();

            if (count >= 2) {
                System.out.println(year);
                return;
            }

            if (count == 0) {
                System.out.println(0);
                return;
            }

            melt();
            year++;
        }
    }

    static void bfs(int x, int y) {
        Queue<int[]> q = new LinkedList<>();
        q.offer(new int[]{x, y});
        visited[x][y] = true;

        while (!q.isEmpty()) {
            int[] now = q.poll();
            for (int d = 0; d < 4; d++) {
                int dy = now[0] + dir[d][0];
                int dx = now[1] + dir[d][1];

                if (dy >= 0 && dx >= 0 && dy < n && dx < m) {
                    if (map[dy][dx] > 0 && !visited[dy][dx]) {
                        visited[dy][dx] = true;
                        q.offer(new int[]{dy, dx});
                    }
                }
            }
        }
    }

    static int countice() {
        visited = new boolean[n][m];
        int count = 0;

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (map[i][j] > 0 && !visited[i][j]) {
                    bfs(i, j);
                    count++;
                }
            }
        }
        return count;
    }

    static void melt() {
        meltcount = new int[n][m];

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (map[i][j] > 0) {
                    int sea = 0;
                    for (int d = 0; d < 4; d++) {
                        int dy = i + dir[d][0];
                        int dx = j + dir[d][1];
                        if (dy >= 0 && dx >= 0 && dy < n && dx < m) {
                            if (map[dy][dx] == 0)
                                sea++;
                        }
                    }
                    meltcount[i][j] = sea;
                }
            }
        }

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                map[i][j] -= meltcount[i][j];
                if (map[i][j] < 0)
                    map[i][j] = 0;
            }
        }
    }
}
```
