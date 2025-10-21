```java
import java.io.*;
import java.util.*;

public class Main {

    static int n, m, x, y, k;
    static int[][] map;
    static int[] dx = {0, 0, 0, -1, 1}; // 동 서 북 남
    static int[] dy = {0, 1, -1, 0, 0};
    static int[] dice = {0, 0, 0, 0, 0, 0}; // 상 하 동 서 북 남

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());
        x = Integer.parseInt(st.nextToken());
        y = Integer.parseInt(st.nextToken());
        k = Integer.parseInt(st.nextToken());

        map = new int[n][m];

        for (int i = 0; i < n; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < m; j++) {
                map[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        st = new StringTokenizer(br.readLine());
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < k; i++) {
            int op = Integer.parseInt(st.nextToken());
            int nx = x + dx[op];
            int ny = y + dy[op];

            if (nx >= n || nx < 0 || ny >= m || ny < 0)
                continue;

            x = nx;
            y = ny;

            switch (op) {
                case 1:
                    move_1();
                    copy(nx, ny);
                    sb.append(dice[0]).append("\n");
                    break;
                case 2:
                    move_2();
                    copy(nx, ny);
                    sb.append(dice[0]).append("\n");
                    break;
                case 3:
                    move_3();
                    copy(nx, ny);
                    sb.append(dice[0]).append("\n");
                    break;
                case 4:
                    move_4();
                    copy(nx, ny);
                    sb.append(dice[0]).append("\n");
                    break;
            }
        }
        System.out.println(sb.toString());
    }

    static void move_1() {
        int temp = dice[0];
        dice[0] = dice[3];
        dice[3] = dice[1];
        dice[1] = dice[2];
        dice[2] = temp;
    }

    static void move_2() {
        int temp = dice[0];
        dice[0] = dice[2];
        dice[2] = dice[1];
        dice[1] = dice[3];
        dice[3] = temp;
    }

    static void move_3() {
        int temp = dice[0];
        dice[0] = dice[5];
        dice[5] = dice[1];
        dice[1] = dice[4];
        dice[4] = temp;
    }

    static void move_4() {
        int temp = dice[0];
        dice[0] = dice[4];
        dice[4] = dice[1];
        dice[1] = dice[5];
        dice[5] = temp;
    }

    static void copy(int cx, int cy) {
        if (map[cx][cy] == 0) {
            map[cx][cy] = dice[1];
        } else {
            dice[1] = map[cx][cy];
            map[cx][cy] = 0;
        }
    }
}
```
