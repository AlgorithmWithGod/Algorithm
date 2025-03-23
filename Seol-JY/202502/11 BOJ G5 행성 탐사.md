```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int M = nextInt(st);
        int N = nextInt(st);
        int[][][] dp = new int[M+1][N+1][3];

        int K = Integer.parseInt(br.readLine());

        for (int i = 1; i < M + 1; i++) {
            String input = br.readLine();
            for (int j = 1; j < N + 1; j++) {
                char target = input.charAt(j - 1);
                // J O I
                int idx = target == 'J' ? 0 : (target == 'O' ? 1 : 2);

                dp[i][j][0] = dp[i-1][j][0] + dp[i][j-1][0] - dp[i-1][j-1][0];
                dp[i][j][1] = dp[i-1][j][1] + dp[i][j-1][1] - dp[i-1][j-1][1];
                dp[i][j][2] = dp[i-1][j][2] + dp[i][j-1][2] - dp[i-1][j-1][2];

                dp[i][j][idx]++;
            }
        }
        
        for (int i = 0; i < K; i++) {
            st = new StringTokenizer(br.readLine());

            int x1 = nextInt(st);
            int y1 = nextInt(st);
            int x2 = nextInt(st);
            int y2 = nextInt(st);

            for(int j = 0; j < 3; j++) {
                System.out.print(dp[x2][y2][j] - dp[x1-1][y2][j] - dp[x2][y1-1][j] + dp[x1-1][y1-1][j] + " "); 
            }
            System.out.println();
        }


    }
    private static int nextInt(StringTokenizer st) {
        return Integer.parseInt(st.nextToken());
    }
}
```
