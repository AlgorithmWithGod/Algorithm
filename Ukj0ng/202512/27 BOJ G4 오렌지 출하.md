```
import java.io.*;
import java.util.Arrays;
import java.util.StringTokenizer;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final long INF = (long)2e14;
    private static long[] dp;
    private static int[] oranges;
    private static int N, M, K;

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
        M = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());

        oranges = new int[N+1];
        dp = new long[N+1];
        for (int i = 1; i <= N; i++) {
            oranges[i] = Integer.parseInt(br.readLine());
        }

        Arrays.fill(dp, INF);
        dp[0] = 0;

        for (int i = 1; i <= N; i++) {
            long max = Long.MIN_VALUE;
            long min = Long.MAX_VALUE;

            for (int j = i; j >= Math.max(1, i-M+1); j--) {
                max = Math.max(max, oranges[j]);
                min = Math.min(min, oranges[j]);
                long cost = K+(i-j+1)*(max-min);
                dp[i] = Math.min(dp[i], dp[j-1]+cost);
            }
        }
    }
}
```
