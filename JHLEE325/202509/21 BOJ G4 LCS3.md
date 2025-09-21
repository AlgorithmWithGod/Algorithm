```java
import java.io.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String a = br.readLine();
        String b = br.readLine();
        String c = br.readLine();

        int alength = a.length();
        int blength = b.length();
        int clength = c.length();

        int[][][] dp = new int[alength + 1][blength + 1][clength + 1];

        for (int i = 1; i <= alength; i++) {
            for (int j = 1; j <= blength; j++) {
                for (int k = 1; k <= clength; k++) {
                    if (a.charAt(i - 1) == b.charAt(j - 1) && b.charAt(j - 1) == c.charAt(k - 1)) {
                        dp[i][j][k] = dp[i - 1][j - 1][k - 1] + 1;
                    } else {
                        dp[i][j][k] = Math.max(dp[i - 1][j][k],
                                Math.max(dp[i][j - 1][k], dp[i][j][k - 1]));
                    }
                }
            }
        }

        System.out.println(dp[alength][blength][clength]);
    }
}
```
