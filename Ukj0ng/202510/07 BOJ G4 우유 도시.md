```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int[] dx = {1, 0};
    private static final int[] dy = {0, 1};
    private static int[][] map;
    private static int[][][] dp;
    private static int N;

    public static void main(String[] args) throws IOException {
        init();
        DP();

        int answer = 0;
        for (int i = 0; i < 3; i++) {
            answer = Math.max(answer, dp[N-1][N-1][i]);
        }
        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        map = new int[N][N];
        dp = new int[N][N][3];

        for (int i = 0; i < N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            for (int j = 0; j < N; j++) {
                map[i][j] = Integer.parseInt(st.nextToken());
                Arrays.fill(dp[i][j], -1);
            }
        }
    }

    private static void DP() {
        if (map[0][0] == 0) dp[0][0][0] = 1;
        dp[0][0][2] = 0;

        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                for (int k = 0; k < 3; k++) {
                    if (dp[i][j][k] == -1) continue;

                    for (int l = 0; l < 2; l++) {
                        int nx = i + dx[l];
                        int ny = j + dy[l];

                        if (OOB(nx, ny)) continue;

                        dp[nx][ny][k] = Math.max(dp[nx][ny][k], dp[i][j][k]);
                        
                        int next = (k+1)%3;
                        if (map[nx][ny] == next) {
                            dp[nx][ny][next] = Math.max(dp[nx][ny][next], dp[i][j][k]+1);
                        }
                    }
                }
            }
        }
    }

    private static boolean OOB(int nx, int ny) {
        return nx < 0 || nx > N-1 || ny < 0 || ny > N-1;
    }
}
```
