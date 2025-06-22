```java
import java.io.*;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N;
    static int[][] cost;
    static int[][] dp;

    public static void main(String[] args) throws IOException {
        N = Integer.parseInt(br.readLine());
        cost = new int[N][N];
        dp = new int[1 << N][N];

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < N; j++) {
                cost[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        for (int i = 0; i < (1 << N); i++) {
            Arrays.fill(dp[i], Integer.MAX_VALUE);
        }

        dp[1][0] = 0;

        for (int i = 1; i < (1 << N); i++) {
            for (int j = 0; j < N; j++) {
                if ((i & (1 << j)) == 0) continue;
                if (dp[i][j] == Integer.MAX_VALUE) continue;

                for (int k = 0; k < N; k++) {
                    if ((i & (1 << k)) != 0) continue;
                    if (cost[j][k] == 0) continue;

                    dp[i | (1 << k)][k] = Math.min(dp[i | (1 << k)][k], dp[i][j] + cost[j][k]);
                }
            }
        }

        int answer = Integer.MAX_VALUE;

        for (int i = 1; i < N; i++) {
            if (dp[(1 << N) - 1][i] != Integer.MAX_VALUE && cost[i][0] != 0) {
                answer = Math.min(answer, dp[(1 << N) - 1][i] + cost[i][0]);
            }
        }

        bw.write(answer + "");
        bw.close();
    }
}
```
