```java
import java.io.*;
import java.util.Arrays;
import java.util.StringTokenizer;

public class BJ_14863_서울에서_경산까지 {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int N, K, ans;
    private static int[][] dp, cost;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());

        cost = new int[N + 1][4];
        for (int i = 1; i <= N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < 4; j++) {
                cost[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        dp = new int[N + 1][K + 1];
        for (int i = 0; i <= N; i++) {
            Arrays.fill(dp[i], -1);
        }
        dp[0][0] = 0;
    }

    private static void sol() throws IOException {
        for (int i = 1; i <= N; i++) {
            for (int j = 0; j <= K; j++) {
                // 도보 선택
                if (j >= cost[i][0] && dp[i - 1][j - cost[i][0]] != -1) {
                    dp[i][j] = Math.max(dp[i][j], dp[i - 1][j - cost[i][0]] + cost[i][1]);
                }

                // 자전거 선택
                if (j >= cost[i][2] && dp[i - 1][j - cost[i][2]] != -1) {
                    dp[i][j] = Math.max(dp[i][j], dp[i - 1][j - cost[i][2]] + cost[i][3]);
                }
            }
        }

        for (int i = 0; i <= K; i++) {
            if (dp[N][i] != -1) {
                ans = Math.max(ans, dp[N][i]);
            }
        }

        bw.write(ans + "");
        bw.flush();
        bw.close();
        br.close();
    }

}
```