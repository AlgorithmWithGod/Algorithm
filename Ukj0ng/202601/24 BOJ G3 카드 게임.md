```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[][] dp;
    private static int[] arr;
    private static int N;

    public static void main(String[] args) throws IOException {
        int T = Integer.parseInt(br.readLine());

        while (T-->0) {
            init();
            int answer = DP(1, N, true);
            bw.write(answer + "\n");
        }
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        arr = new int[N+1];
        dp = new int[N+1][N+1];

        StringTokenizer st = new StringTokenizer(br.readLine());

        for (int i = 1; i <= N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
            Arrays.fill(dp[i], -1);
        }
    }

    private static int DP(int left, int right, boolean isGeunWoo) {
        if (left > right) return 0;

        if (dp[left][right] != -1) return dp[left][right];

        if (isGeunWoo) {
            int pickLeft = arr[left] + DP(left+1, right, false);
            int pickRight = arr[right] + DP(left, right-1, false);
            return dp[left][right] = Math.max(pickLeft, pickRight);
        } else {
            int pickLeft = DP(left+1, right, true);
            int pickRight = DP(left, right-1, true);
            return dp[left][right] = Math.min(pickLeft, pickRight);
        }
    }
}
```
