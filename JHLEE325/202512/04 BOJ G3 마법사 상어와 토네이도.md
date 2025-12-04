```java
import java.io.*;
import java.util.*;

public class Main {

    static int N;
    static int[][] A;
    static int answer;

    static int[] dx = {0, 1, 0, -1};
    static int[] dy = {-1, 0, 1, 0};

    static int[][] dsx = {
            { -1,  1, -2, -1,  1,  2, -1,  1,  0 },
            { -1, -1,  0,  0,  0,  0,  1,  1,  2 },
            {  1, -1,  2,  1, -1, -2,  1, -1,  0 },
            {  1,  1,  0,  0,  0,  0, -1, -1, -2 }
    };

    static int[][] dsy = {
            {  1,  1,  0,  0,  0,  0, -1, -1, -2 },
            { -1,  1, -2, -1,  1,  2, -1,  1,  0 },
            { -1, -1,  0,  0,  0,  0,  1,  1,  2 },
            {  1, -1,  2,  1, -1, -2,  1, -1,  0 }
    };

    static int[] ratio = {1, 1, 2, 7, 7, 2, 10, 10, 5};

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        N = Integer.parseInt(br.readLine());
        A = new int[N][N];

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < N; j++) {
                A[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        simulate();
        System.out.println(answer);
    }

    static void simulate() {
        int x = N/2;
        int y = N/2;

        int len = 1;
        int dir = 0;

        while (true) {
            for (int i = 0; i < 2; i++) {
                for (int step = 0; step < len; step++) {

                    x += dx[dir];
                    y += dy[dir];

                    spread(x, y, dir);

                    if (x == 0 && y == 0) return;
                }
                dir = (dir + 1) % 4;
            }
            len++;
        }
    }

    static void spread(int x, int y, int dir) {
        int sand = A[x][y];
        if (sand == 0) {
            return;
        }
        A[x][y] = 0;

        int used = 0;

        for (int i = 0; i < 9; i++) {
            int nx = x + dsx[dir][i];
            int ny = y + dsy[dir][i];

            int amount = (sand * ratio[i]) / 100;
            used += amount;

            if (nx < 0 || ny < 0 || nx >= N || ny >= N) {
                answer += amount;
            } else {
                A[nx][ny] += amount;
            }
        }

        int ax = x + dx[dir];
        int ay = y + dy[dir];
        int remain = sand - used;

        if (ax < 0 || ay < 0 || ax >= N || ay >= N) {
            answer += remain;
        } else {
            A[ax][ay] += remain;
        }
    }
}
```
