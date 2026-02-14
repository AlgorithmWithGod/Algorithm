```java
import java.io.*;
import java.util.HashSet;
import java.util.Set;
import java.util.StringTokenizer;

public class BJ_17135_캐슬_디펜스 {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int N, M, D, ans;
    private static int[]   archers;
    private static int[][] map, grid;
    private static Set<Integer> targets;

    public static void main(String[] args) throws IOException {
        init();
        sol();

        bw.write(ans + "");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        D = Integer.parseInt(st.nextToken());

        map = new int[N][M];
        grid = new int[N][M];

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < M; j++) {
                map[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        archers = new int[3];
        targets = new HashSet<>();
    }

    private static void sol() {
        for (int i = 0; i < M; i++) {
            for (int j = i + 1; j < M; j++) {
                for (int k = j + 1; k < M; k++) {
                    archers[0] = i;
                    archers[1] = j;
                    archers[2] = k;

                    ans = Math.max(ans, simulate());
                }
            }
        }
    }

    private static int simulate() {
        for (int i = 0; i < N; i++) {
            grid[i] = map[i].clone();
        }

        int killed = 0;
        for (int archerRow = N; archerRow >= 1; archerRow--) {
            targets.clear();

            for (int i = 0; i < 3; i++) {
                findTarget(archerRow, archers[i]);
            }

            for (int target : targets) {
                int row = target / M;
                int col = target % M;
                if (grid[row][col] == 1) {
                    grid[row][col] = 0;
                    killed++;
                }
            }
        }

        return killed;
    }

    private static void findTarget(int archerRow, int archerCol) {
        int targetRow = -1;
        int targetCol = -1;
        int minDist   = Integer.MAX_VALUE;

        for (int row = archerRow - 1; row >= 0; row--) {
            for (int col = 0; col < M; col++) {
                if (grid[row][col] == 0) continue;

                int dist = Math.abs(archerRow - row) + Math.abs(archerCol - col);
                if (dist > D) continue;

                if (dist < minDist || (dist == minDist && col < targetCol)) {
                    minDist = dist;
                    targetRow = row;
                    targetCol = col;
                }
            }
        }

        if (targetRow != -1) {
            targets.add(targetRow * M + targetCol);
        }
    }

}
```