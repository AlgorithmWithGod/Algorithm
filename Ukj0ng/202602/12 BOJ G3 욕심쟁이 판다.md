```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int[] dx = {1, 0, -1, 0};
    private static final int[] dy = {0, 1, 0, -1};
    private static int[][] map;
    private static int[][] dp;
    private static int N, answer;

    public static void main(String[] args) throws IOException {
        init();

        for (int i = 1; i <= N; i++) {
            for (int j = 1; j <= N; j++) {
                answer = Math.max(answer, DFS(i, j));
            }
        }

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        map = new int[N+1][N+1];
        dp = new int[N+1][N+1];

        for (int i = 1; i <= N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            for (int j = 1; j <= N; j++) {
                map[i][j] = Integer.parseInt(st.nextToken());
            }
        }
    }

    private static int DFS(int x, int y) {
        if (dp[x][y] != 0) return dp[x][y];

        dp[x][y] = 1;

        for (int i = 0; i < 4; i++) {
            int nx = x + dx[i];
            int ny = y + dy[i];

            if (OOB(nx, ny)) continue;

            if (map[nx][ny] > map[x][y]) {
                dp[x][y] = Math.max(dp[x][y], DFS(nx, ny) + 1);
            }
        }
        
        return dp[x][y];
    }

    private static boolean OOB(int nx, int ny) {
        return nx < 1 || nx > N || ny < 1 || ny > N;
    }
}
```
