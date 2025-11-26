```java
import java.io.*;
import java.util.StringTokenizer;

public class BJ_14722_우유_도시 {

    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static StringTokenizer st;

    private static int N;
    private static int[][] milk;
    private static Milk[][] dp;

    private static class Milk {
        int prev;
        int cnt;

        Milk(int prev, int cnt) {
            this.prev = prev;
            this.cnt = cnt;
        }
    }

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        milk = new int[N + 1][N + 1];
        dp = new Milk[N + 1][N + 1];

        for (int i = 1; i <= N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 1; j <= N; j++) {
                milk[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        for (int i = 0; i <= N; i++) {
            for (int j = 0; j <= N; j++) {
                dp[i][j] = new Milk(0, 0);
            }
        }
    }

    private static void sol() throws IOException {
        for (int i = 1; i <= N; i++) {
            for (int j = 1; j <= N; j++) {
                Milk fromUp = dp[i - 1][j];
                Milk fromLeft = dp[i][j - 1];
                Milk better = fromUp.cnt >= fromLeft.cnt ? fromUp : fromLeft;

                if (milk[i][j] == better.prev) {
                    dp[i][j] = new Milk((better.prev + 1) % 3, better.cnt + 1);
                } else {
                    dp[i][j] = new Milk(better.prev, better.cnt);
                }
            }
        }

        bw.write(dp[N][N].cnt + "");
        bw.flush();
        bw.close();
        br.close();
    }
}
```