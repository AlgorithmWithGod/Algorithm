```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int INF = (int)1e9 + 7;
    private static int[][] dp;
    private static int s;
    private static String input;

    public static void main(String[] args) throws IOException {
        init();
        int answer = dp[input.length()][s];
        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        s = Integer.parseInt(br.readLine());
        input = br.readLine();
        dp = new int[input.length()+1][s+1];

        dp[0][0] = 1;

        for (int i = 0; i <= input.length(); i++) {
            for (int j = i; j <= s; j++) {
                int temp = dp[i][j-1] + dp[i-1][j];
                if (j >= 26) temp -= dp[i-1][j-26];
                temp %= INF;
                if (temp < 0) temp += INF;
                dp[i][j] = temp;
            }
        }
    }
}
```
