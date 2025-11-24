```java
import java.io.*;
import java.util.StringTokenizer;

public class BJ_G3_비트코인은_신이고_나는_무적이다 {

    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static StringTokenizer st;

    private static int N, M;
    private static int[] candlestick;
    private static boolean[][] dp;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        candlestick = new int[N + 1];
        st = new StringTokenizer(br.readLine());
        for (int i = 1; i <= N; i++) {
            candlestick[i] = Math.abs(Integer.parseInt(st.nextToken()));
        }
        dp = new boolean[M + 1][1024];
        dp[0][0] = true;
    }

    private static void sol() throws IOException {
        for (int i = 0; i < M; i++) {
            for (int j = 0; j < 1024; j++) {
                if (dp[i][j]) {
                    for (int k = 1; k <= N; k++) {
                        dp[i + 1][j ^ candlestick[k]] = true;
                    }
                }
            }
        }

        for (int j = 1023; j >= 0; j--) {
            if (dp[M][j]) {
                bw.write(j + "");
                break;
            }
        }

        bw.flush();
        bw.close();
        br.close();
    }

}
```