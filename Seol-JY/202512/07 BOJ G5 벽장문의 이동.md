```java
import java.io.*;
import java.util.*;

public class Main {
    static int n, m;
    static int[] order;
    static int[][][] dp;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        n = Integer.parseInt(br.readLine().trim());
        StringTokenizer st = new StringTokenizer(br.readLine());
        int open1 = Integer.parseInt(st.nextToken());
        int open2 = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(br.readLine().trim());
        order = new int[m];
        for (int i = 0; i < m; i++) {
            order[i] = Integer.parseInt(br.readLine().trim());
        }

        dp = new int[m + 1][n + 1][n + 1];
        for (int[][] arr2d : dp) {
            for (int[] arr1d : arr2d) {
                Arrays.fill(arr1d, -1);
            }
        }

        System.out.println(solve(0, open1, open2));
    }

    static int solve(int idx, int a, int b) {
        if (idx == m) return 0;
        if (dp[idx][a][b] != -1) return dp[idx][a][b];

        int target = order[idx];
        int moveA = Math.abs(target - a) + solve(idx + 1, target, b);
        int moveB = Math.abs(target - b) + solve(idx + 1, a, target);

        return dp[idx][a][b] = Math.min(moveA, moveB);
    }
}
```
