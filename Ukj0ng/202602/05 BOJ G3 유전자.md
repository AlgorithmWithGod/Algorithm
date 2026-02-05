```
import java.io.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[][] dp;

    public static void main(String[] args) throws IOException {
        init();

        bw.write(dp[1][dp[0].length-2] + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        char[] input = br.readLine().toCharArray();

        dp = new int[input.length+2][input.length+2];

        int left = 0;
        int right = 1;

        while (left <= input.length-2) {
            if (input[left] == 'a' && input[right] == 't') dp[left+1][right+1] = 2;
            if (input[left] == 'g' && input[right] == 'c') dp[left+1][right+1] = 2;
            left++;
            right++;
        }


        for (int len = 3; len <= input.length; len++) {
            for (int i = 1; i+len-1 <= input.length; i++) {
                if ((input[i-1] == 'a' && input[i-2+len] == 't')
                        || (input[i-1] == 'g' && input[i-2+len] == 'c')) {
                    dp[i][i+len-1] = dp[i+1][i+len-2]+2;
                }
                for (int j = i; j < i+len-1; j++) {
                    dp[i][i+len-1] = Math.max(dp[i][i+len-1], dp[i][j] + dp[j+1][i+len-1]);
                }
            }
        }
    }
}
```
