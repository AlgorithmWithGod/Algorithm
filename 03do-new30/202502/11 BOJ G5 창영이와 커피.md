```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        StringTokenizer st = new StringTokenizer(br.readLine());
        int N = Integer.parseInt(st.nextToken());
        int K = Integer.parseInt(st.nextToken());

        int[] cups = new int[N+1];
        st = new StringTokenizer(br.readLine());
        for (int i = 1; i < N+1; i++) {
            cups[i] = Integer.parseInt(st.nextToken());
        }

        // dp[i][j] = 카페인 i를 채우기 위해 커피 j까지 고려했을 때 최소 잔 수
        int[][] dp = new int[K+1][N+1];

        // 초기화
        int maxCups = 101;
        for (int i = 0; i < K+1; i++) {
            for (int j = 0; j < N+1; j++) {
                if (i == 0) {
                    dp[i][j] = 0;
                    continue;
                }
                dp[i][j] = maxCups;
            }
        }

        for (int caffeine = 1; caffeine < K+1; caffeine++) {
            for (int coffee = 1; coffee < N+1; coffee++) {
                // (default) coffee번째 커피를 마시지 않는다면, caffine을 채우기 위해 coffee-1번째 커피까지 고려했을 때의 최소값이 dp[caffeine][coffee]가 됨
                dp[caffeine][coffee] = dp[caffeine][coffee-1];
                // coffee번째 커피를 마시는 경우
                if (caffeine - cups[coffee] >= 0) {
                    dp[caffeine][coffee] = Integer.min(dp[caffeine][coffee], dp[caffeine-cups[coffee]][coffee-1] + 1);
                }
            }
        }

        int answer = dp[K][N];
        if (answer == maxCups) {
            answer = -1;
        }
        bw.write(answer + "\n");

        br.close();
        bw.flush();
        bw.close();
    }
}

```
