```java
import java.awt.*;
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
    static int height, width;
    static int[][] arr;
    static int[][] dp;

    public static void main(String[] args) throws IOException {
        init();
        int result = process();
        System.out.println(result * result);
    }

    private static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        height = Integer.parseInt(st.nextToken());
        width = Integer.parseInt(st.nextToken());

        arr = new int[height][width];
        dp = new int[height][width];

        for (int i = 0; i < height; i++) {
            String[] input = br.readLine().split("");
            for (int j = 0; j < width; j++) {
                arr[i][j] = Integer.parseInt(input[j]);
            }
        }
    }

    private static int process() {
        int maxSize = 0;

        // DP 초기화 및 계산
        for (int i = 0; i < height; i++) {
            for (int j = 0; j < width; j++) {
                if (arr[i][j] == 1) {
                    if (i == 0 || j == 0) {
                        dp[i][j] = 1;
                    } else {
                        //  왼쪽, 위쪽, 대각선 위쪽의 최솟값 + 1
                        dp[i][j] = Math.min(dp[i-1][j],
                                Math.min(dp[i][j-1], dp[i-1][j-1])) + 1;
                    }
                    maxSize = Math.max(maxSize, dp[i][j]);
                } else {
                    dp[i][j] = 0;
                }
            }
        }

        return maxSize;
    }
}
```