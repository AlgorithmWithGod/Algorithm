```java
import java.io.*;
import java.util.StringTokenizer;

public class BJ_1937_욕심쟁이_판다 {

    private static final int[] dx = { 0, 1, 0, -1 };
    private static final int[] dy = { 1, 0, -1, 0 };

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int N, ans;
    private static int[][] bamboo, dp;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        ans = 0;

        bamboo = new int[N][N];
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < N; j++) {
                bamboo[i][j] = Integer.parseInt(st.nextToken());
            }
        }
        dp = new int[N][N];
    }

    private static void sol() throws IOException {
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                ans = Math.max(ans, dfs(i, j));
            }
        }
        bw.write(ans + "");
        bw.flush();
        bw.close();
        br.close();
    }

    private static int dfs(int x, int y) {
        if (dp[x][y] != 0) return dp[x][y];

        dp[x][y] = 1;

        for (int d = 0; d < 4; d++) {
            int nx = x + dx[d];
            int ny = y + dy[d];

            if (OOB(nx, ny) || bamboo[x][y] >= bamboo[nx][ny]) continue;

            dp[x][y] = Math.max(dp[x][y], dfs(nx, ny) + 1);
        }
        return dp[x][y];
    }

    private static boolean OOB(int x, int y) {
        return x < 0 || x >= N || y < 0 || y >= N;
    }

}
```