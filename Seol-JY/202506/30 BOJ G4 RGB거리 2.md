```java
import java.io.*;
import java.util.*; 

public class Main {
    static final int RED = 0;
    static final int GREEN = 1;
    static final int BLUE = 2;
    
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        
        int[][] cost = new int[n][3];
        for (int i = 0; i < n; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            cost[i][RED] = Integer.parseInt(st.nextToken());
            cost[i][GREEN] = Integer.parseInt(st.nextToken());
            cost[i][BLUE] = Integer.parseInt(st.nextToken());
        }
        
        int answer = 987654321;
        
        for (int firstColor = 0; firstColor < 3; firstColor++) {
            int[][] dp = new int[n][3];
            
            for (int j = 0; j < 3; j++) {
                if (j == firstColor) {
                    dp[0][j] = cost[0][j];
                } else {
                    dp[0][j] = 987654321;
                }
            }
            
            for (int i = 1; i < n; i++) {
                dp[i][RED] = Math.min(dp[i-1][GREEN], dp[i-1][BLUE]) + cost[i][RED];
                dp[i][GREEN] = Math.min(dp[i-1][RED], dp[i-1][BLUE]) + cost[i][GREEN];
                dp[i][BLUE] = Math.min(dp[i-1][RED], dp[i-1][GREEN]) + cost[i][BLUE];
            }
            
            for (int j = 0; j < 3; j++) {
                if (j != firstColor) {
                    answer = Math.min(answer, dp[n-1][j]);
                }
            }
        }
        
        System.out.println(answer);
    }
}
```
