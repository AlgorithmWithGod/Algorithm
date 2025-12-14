```java
import java.io.*;
import java.util.*;

public class Main {

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int W = Integer.parseInt(st.nextToken());
        int H = Integer.parseInt(st.nextToken());

        int[][][][] dp = new int[W + 1][H + 1][2][2];

        if (W >= 2) dp[2][1][0][0] = 1;
        if (H >= 2) dp[1][2][1][0] = 1;

        for (int x = 1; x <= W; x++) {
            for (int y = 1; y <= H; y++) {

                if (x > 1) {
                    dp[x][y][0][0] = (dp[x][y][0][0] + dp[x - 1][y][0][0] + dp[x - 1][y][0][1]) % 100000;

                    dp[x][y][0][1] = (dp[x][y][0][1] + dp[x - 1][y][1][0]) % 100000;
                }

                if (y > 1) {
                    dp[x][y][1][0] = (dp[x][y][1][0] + dp[x][y - 1][1][0] + dp[x][y - 1][1][1]) % 100000;

                    dp[x][y][1][1] = (dp[x][y][1][1] + dp[x][y - 1][0][0]) % 100000;
                }
            }
        }

        int answer = 0;
        for (int d = 0; d < 2; d++) {
            for (int t = 0; t < 2; t++) {
                answer = (answer + dp[W][H][d][t]) % 100000;
            }
        }

        System.out.println(answer);
    }
}
```
