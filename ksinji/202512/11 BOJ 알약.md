```java
import java.io.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        long[][] dp = new long[31][31];

        for (int h = 0; h <= 30; h++) {
            dp[0][h] = 1;
        }

        for (int w = 1; w <= 30; w++) {
            for (int h = 0; h <= 30; h++) {
                long v = 0;

                if (w > 0 && h < 30) {
                    v += dp[w - 1][h + 1];
                }

                if (h > 0) {
                    v += dp[w][h - 1];
                }

                dp[w][h] = v;
            }
        }

        StringBuilder sb = new StringBuilder();
        while (true) {
            String line = br.readLine();
            if (line == null || line.isEmpty()) break;

            int n = Integer.parseInt(line);
            if (n == 0) break;

            sb.append(dp[n][0]).append('\n');
        }

        System.out.print(sb);
    }
}
