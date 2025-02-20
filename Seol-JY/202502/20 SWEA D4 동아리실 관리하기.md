```java
import java.io.*;

public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int testCases = Integer.parseInt(br.readLine());
        for (int tc = 1; tc <= testCases; tc++) {
            String sequence = br.readLine();
            System.out.println("#" + tc + " " + solve(sequence, sequence.length()));
        }
    }

    private static int solve(String sequence, int length) {
        int[][] dp = new int[16][length];
        final int MOD = 1_000_000_007;

        int firstState = (1 << (sequence.charAt(0) - 'A')) | 1;
        for (int state = 1; state <= 15; state++) {
            if ((state & firstState) == firstState) {
                dp[state][0] = 1;
            }
        }

        for (int pos = 1; pos < length; pos++) {
            int currentPerson = 1 << (sequence.charAt(pos) - 'A');
            for (int currState = 1; currState <= 15; currState++) {
                if ((currState & currentPerson) == currentPerson) {
                    for (int prevState = 1; prevState <= 15; prevState++) {
                        if (dp[prevState][pos-1] > 0 && ((currState & prevState) > 0)) {
                            dp[currState][pos] = (dp[currState][pos] + dp[prevState][pos-1]) % MOD;
                        }
                    }
                }
            }
        }

        int result = 0;
        for (int state = 1; state <= 15; state++) {
            result = (result + dp[state][length-1]) % MOD;
        }
        return result;
    }
}
```
