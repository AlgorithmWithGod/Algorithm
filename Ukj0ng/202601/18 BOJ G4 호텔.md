```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[] dp;
    private static int[][] cites;
    private static int N, C;

    public static void main(String[] args) throws IOException {
        init();

        bw.write(dp[N] + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        C = Integer.parseInt(st.nextToken());

        cites = new int[C][2];
        dp = new int[N+1];

        for (int i = 0; i < C; i++) {
            st = new StringTokenizer(br.readLine());
            cites[i][0] = Integer.parseInt(st.nextToken());
            cites[i][1] = Integer.parseInt(st.nextToken());
        }

        Arrays.fill(dp, Integer.MAX_VALUE);
        dp[0] = 0;

        for (int i = 0; i < C; i++) {
            for (int j = 1; j < N; j++) {
                if (j - cites[i][1] >= 0 && dp[j - cites[i][1]] != Integer.MAX_VALUE) {
                    dp[j] = Math.min(dp[j], dp[j - cites[i][1]] + cites[i][0]);
                }
            }

            for (int j = N - cites[i][1]; j <= N; j++) {
                if (j >= 0 && dp[j] != Integer.MAX_VALUE) dp[N] = Math.min(dp[N], dp[j] + cites[i][0]);
            }
        }
    }
}
```
