```
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[][] dp;
    private static int[] arr;
    private static int N, V;

    public static void main(String[] args) throws IOException {
        init();
        int answer = dp[3][N];

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        StringTokenizer st = new StringTokenizer(br.readLine());
        arr = new int[N+1];
        dp = new int[4][N+1];

        for (int i = 1; i <= N; i++) {
            arr[i] = arr[i-1] + Integer.parseInt(st.nextToken());
        }

        V = Integer.parseInt(br.readLine());

        for (int i = 1; i <= 3; i++) {
            for (int j = V; j <= N; j++) {
                dp[i][j] = Math.max(dp[i][j-1], arr[j] - arr[j-V] + dp[i-1][j-V]);
            }
        }
    }
}
```
