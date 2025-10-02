```java
import java.io.*;
import java.util.StringTokenizer;

public class BJ_2600_구슬게임 {

    private static final boolean A = true;
    private static final boolean B = false;

    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final StringBuilder sb = new StringBuilder();
    private static StringTokenizer st;

    private static int[] beads;
    private static boolean[][] dp;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());

        beads = new int[3];
        for (int i = 0; i < 3; i++) {
            beads[i] = Integer.parseInt(st.nextToken());
        }

        dp = new boolean[501][501];
    }

    private static void sol() throws IOException {
        for (int i = 0; i < 501; i++) {
            for (int j = 0; j < 501; j++) {
                if (i == 0 && j == 0) {
                    dp[i][j] = B;
                    continue;
                }

                boolean whoWins = B;

                // 첫 번째 구슬
                for (int bead : beads) {
                    if (i >= bead && !dp[i - bead][j]) {
                        whoWins = A;
                        break;
                    }
                }

                // 두 번째 구슬
                for (int bead : beads) {
                    if (j >= bead && !dp[i][j - bead]) {
                        whoWins = A;
                        break;
                    }
                }

                dp[i][j] = whoWins;
            }
        }
        for (int i = 0; i < 5; i++) {
            st = new StringTokenizer(br.readLine());

            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());

            sb.append(dp[a][b] ? "A\n" : "B\n");
        }
        bw.write(sb.toString());
        bw.flush();
        bw.close();
        br.close();
    }

}
```