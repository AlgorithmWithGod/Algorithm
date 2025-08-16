```java
import java.io.*;
import java.util.*;

public class Main {

    static int NEG_INF = Integer.MIN_VALUE / 4;
    static int size,groupCnt;
    static int[] a;

    public static void main(String[] args) throws Exception {
        init();
        process();

    }

    public static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        size = Integer.parseInt(st.nextToken());
        groupCnt = Integer.parseInt(st.nextToken());

        a = new int[size + 1];
        st = new StringTokenizer(br.readLine());
        for (int i = 1; i <= size; i++) a[i] = Integer.parseInt(st.nextToken());
    }

    public static void process(){

        int[] prefixSum = new int[size + 1];
        for (int i = 1; i <= size; i++) prefixSum[i] = prefixSum[i - 1] + a[i];


        int[][] dp = new int[size + 1][groupCnt + 1];
        for (int i = 0; i <= size; i++) {
            Arrays.fill(dp[i], NEG_INF);
            dp[i][0] = 0;
        }
        dp[0][0] = 0;

        // dp[i][j] = max(dp[i-1][j], max_s(dp[s-1][j-1] + (ps[i]-ps[s-1])))
        //          = max(dp[i-1][j], (max_s(dp[s-1][j-1] - ps[s-1])) + ps[i])
        for (int j = 1; j <= groupCnt; j++) {
            int best = NEG_INF;
            for (int i = 1; i <= size; i++) {
                best = Math.max(best, dp[i - 1][j - 1] - prefixSum[i - 1]);

                dp[i][j] = Math.max(dp[i][j], dp[i - 1][j]);

                if (best > NEG_INF) {
                    dp[i][j] = Math.max(dp[i][j], best + prefixSum[i]);
                }
            }
        }

        System.out.println(dp[size][groupCnt]);
    }
}


```