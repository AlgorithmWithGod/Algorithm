```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[][] map, dp;
    private static int[] wall;
    private static boolean vertical;
    private static int N, M;

    public static void main(String[] args) throws IOException {
        init();
        DP();

        if (dp[N-1][M-1] == -1000000001) bw.write("Entity");
        else bw.write(dp[N-1][M-1] + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        map = new int[N][M];
        dp = new int[N][M];
        wall = new int[4];

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < M; j++) {
                map[i][j] = Integer.parseInt(st.nextToken());
                dp[i][j] = -1000000001;
            }
        }

        st = new StringTokenizer(br.readLine());
        wall[0] = Integer.parseInt(st.nextToken());
        wall[1] = Integer.parseInt(st.nextToken());
        wall[2] = Integer.parseInt(st.nextToken());
        wall[3] = Integer.parseInt(st.nextToken());

        vertical = wall[1] == wall[3];
    }

    private static void DP() {
        dp[0][0] = map[0][0];

        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                if (i == 0 && j == 0) continue;

                if (i > 0 && dp[i-1][j] != -1000000001 && canMove(i-1, j, 0)) {
                    dp[i][j] = Math.max(dp[i][j], dp[i-1][j] + map[i][j]);
                }

                if (j > 0 && dp[i][j-1] != -1000000001 && canMove(i, j-1, 1)) {
                    dp[i][j] = Math.max(dp[i][j], dp[i][j-1] + map[i][j]);
                }
            }
        }
    }

    private static boolean canMove(int x, int y, int dir) {
        if (vertical && dir == 1) {
            int x_min = Math.min(wall[0], wall[2]);
            int x_max = Math.max(wall[0], wall[2]);
            if ((x_min <= x && x < x_max) && y+1 == wall[1]) return false;
        } else if (!vertical && dir == 0) {
            int y_min = Math.min(wall[1], wall[3]);
            int y_max = Math.max(wall[1], wall[3]);
            if (x+1 == wall[0] && (y_min <= y && y < y_max)) return false;
        }
        return true;
    }
}
```
