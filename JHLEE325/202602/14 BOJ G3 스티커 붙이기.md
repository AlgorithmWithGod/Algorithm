```java
import java.io.*;
import java.util.*;

public class Main {

    static int N, M, K;
    static int[][] note;
    static int R, C;
    static int[][] sticker;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());

        note = new int[N][M];

        for (int s = 0; s < K; s++) {
            st = new StringTokenizer(br.readLine());
            R = Integer.parseInt(st.nextToken());
            C = Integer.parseInt(st.nextToken());
            sticker = new int[R][C];

            for (int i = 0; i < R; i++) {
                st = new StringTokenizer(br.readLine());
                for (int j = 0; j < C; j++) sticker[i][j] = Integer.parseInt(st.nextToken());
            }

            for (int d = 0; d < 4; d++) {
                if (tryAttach()) break;
                rotate();
            }
        }

        int count = 0;
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) if (note[i][j] == 1) count++;
        }
        System.out.println(count);
    }

    static boolean tryAttach() {
        for (int i = 0; i <= N - R; i++) {
            for (int j = 0; j <= M - C; j++) {
                if (canAttach(i, j)) {
                    attach(i, j);
                    return true;
                }
            }
        }
        return false;
    }

    static boolean canAttach(int y, int x) {
        for (int i = 0; i < R; i++) {
            for (int j = 0; j < C; j++) {
                if (sticker[i][j] == 1 && note[y + i][x + j] == 1) return false;
            }
        }
        return true;
    }

    static void attach(int y, int x) {
        for (int i = 0; i < R; i++) {
            for (int j = 0; j < C; j++) {
                if (sticker[i][j] == 1) note[y + i][x + j] = 1;
            }
        }
    }

    static void rotate() {
        int[][] temp = new int[C][R];
        for (int i = 0; i < R; i++) {
            for (int j = 0; j < C; j++) {
                temp[j][R - 1 - i] = sticker[i][j];
            }
        }
        sticker = temp;
        int t = R;
        R = C;
        C = t;
    }
}
```
