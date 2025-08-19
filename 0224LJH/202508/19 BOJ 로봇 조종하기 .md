```java

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

public class Main {

    static int height,width,ans;

    static int[][] arr;
    static int[][][] dp;

    static final int TOP = 0;
    static final int LEFT = 1;
    static final int RIGHT = 2;
    static final int MIN = Integer.MIN_VALUE/2;

    public static void main(String[] args) throws IOException {
        init();
        process();
        print();
    }

    private static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        height = Integer.parseInt(st.nextToken());
        width = Integer.parseInt(st.nextToken());
        arr = new int[height][width];
        dp = new int[height][width][3];
        ans = MIN;
        // 합의 최댓값을 직전에 어느 방향에서 왔는지에 따라 구분.
        // 0 ,1 , 2가 순서대로 위,왼,오

        for (int i = 0; i < height; i++){
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < width; j++){
                arr[i][j] = Integer.parseInt(st.nextToken());
                Arrays.fill(dp[i][j], MIN);
            }
        }

    }

    private static void process() throws IOException {
        calculateFirstLine();
        for (int i = 1; i < height; i++){
            calculateFromTop(i);
            calculateFromLeft(i);
            calculateFromRight(i);
        }

        for (int i = 0; i < 3; i++){
            ans = Math.max (ans,dp[height-1][width-1][i]);
        }

    }

    private static void calculateFromRight(int curHeight) {
        dp[curHeight][width-1][RIGHT] = dp[curHeight][width-1][TOP];
        for (int i = width - 2; i >= 0; i--) {
            dp[curHeight][i][RIGHT] = arr[curHeight][i] + Math.max(dp[curHeight][i+1][TOP], dp[curHeight][i+1][RIGHT]);
        }
    }

    private static void calculateFromLeft(int curHeight) {
        dp[curHeight][0][LEFT] = dp[curHeight][0][TOP];
        for (int i = 1; i < width; i++){
            dp[curHeight][i][LEFT] = arr[curHeight][i] + Math.max(dp[curHeight][i-1][TOP],  dp[curHeight][i-1][LEFT]) ;
        }
    }

    private static void calculateFromTop(int curHeight) {
        for (int i = 0; i < width; i++){
            int curLargest = MIN;
            for (int j = 0; j < 3; j++) curLargest = Math.max(curLargest, dp[curHeight-1][i][j]);

            dp[curHeight][i][TOP] = curLargest + arr[curHeight][i];
        }
    }

    private static void calculateFirstLine() {
        int cur = 0;
        for (int i = 0; i < width; i++){
            cur += arr[0][i];
            dp[0][i][0] = cur;
        }
    }


    private static void print() {
        System.out.println(ans);
    }
}
```