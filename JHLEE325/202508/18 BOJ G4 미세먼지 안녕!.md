```java
import java.io.*;
import java.util.*;

public class Main {
    static int r, c, t;
    static int[][] map;
    static int up, down;
    static final int[] dy = {-1, 1, 0, 0};
    static final int[] dx = {0, 0, -1, 1};

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        r = Integer.parseInt(st.nextToken());
        c = Integer.parseInt(st.nextToken());
        t = Integer.parseInt(st.nextToken());

        map = new int[r][c];
        up = down = -1;

        for (int i = 0; i < r; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < c; j++) {
                map[i][j] = Integer.parseInt(st.nextToken());
                if (map[i][j] == -1) {
                    if (up == -1) up = i;
                    else down = i;
                }
            }
        }

        while (t-- > 0) {
            spread();
            purify();
        }

        long sum = 0;
        for (int i = 0; i < r; i++)
            for (int j = 0; j < c; j++)
                if (map[i][j] > 0) sum += map[i][j];

        System.out.println(sum);
    }

    static void spread() {
        int[][] add = new int[r][c];
        for (int y = 0; y < r; y++) {
            for (int x = 0; x < c; x++) {
                if (map[y][x] <= 0) continue;
                int amount = map[y][x] / 5;
                if (amount == 0) continue;

                int cnt = 0;
                for (int d = 0; d < 4; d++) {
                    int ny = y + dy[d], nx = x + dx[d];
                    if (ny < 0 || nx < 0 || ny >= r || nx >= c) continue;
                    if (map[ny][nx] == -1) continue;
                    add[ny][nx] += amount;
                    cnt++;
                }
                map[y][x] -= amount * cnt;
            }
        }
        for (int i = 0; i < r; i++) {
            for (int j = 0; j < c; j++) {
                if (map[i][j] == -1) continue;
                map[i][j] += add[i][j];
            }
        }
    }

    static void purify() {
        for (int i = up - 1; i > 0; i--) map[i][0] = map[i - 1][0];
        for (int j = 0; j < c - 1; j++) map[0][j] = map[0][j + 1];
        for (int i = 0; i < up; i++) map[i][c - 1] = map[i + 1][c - 1];
        for (int j = c - 1; j > 1; j--) map[up][j] = map[up][j - 1];
        map[up][1] = 0;
        map[up][0] = -1;

        for (int i = down + 1; i < r - 1; i++) map[i][0] = map[i + 1][0];
        for (int j = 0; j < c - 1; j++) map[r - 1][j] = map[r - 1][j + 1];
        for (int i = r - 1; i > down; i--) map[i][c - 1] = map[i - 1][c - 1];
        for (int j = c - 1; j > 1; j--) map[down][j] = map[down][j - 1];
        map[down][1] = 0;
        map[down][0] = -1;
    }
}

```
