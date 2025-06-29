```java
import java.util.*;
import java.io.*;
public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N;
    static int[][] cost;
    static int[][] dp;
    
    public static void main(String[] args) throws Exception{
      N = Integer.parseInt(br.readLine());
      cost = new int[N+1][3];
      
      for(int i=1; i<=N;i++){
        st = new StringTokenizer(br.readLine());
        cost[i][0] = Integer.parseInt(st.nextToken());
        cost[i][1] = Integer.parseInt(st.nextToken());
        cost[i][2] = Integer.parseInt(st.nextToken());
      }
      
      int min = Integer.MAX_VALUE;
      for(int firstColor=0; firstColor<3; firstColor++){
        dp = new int[N+1][3];
        dp[1][firstColor] = cost[1][firstColor];
        dp[1][(firstColor+1)%3] = 10000000;
        dp[1][(firstColor+2)%3] = 10000000;
        
        for(int i=2;i<N;i++){
          for(int j = 0;j<3;j++){
            dp[i][j] = Math.min(dp[i-1][(j+1)%3] + cost[i][j], dp[i-1][(j+2)%3] + cost[i][j]);
          }
        }
        dp[N][(firstColor+1)%3] = Math.min(dp[N-1][firstColor]+cost[N][(firstColor+1)%3], dp[N-1][(firstColor+2)%3]+cost[N][(firstColor+1)%3]);
        dp[N][(firstColor+2)%3] = Math.min(dp[N-1][firstColor]+cost[N][(firstColor+2)%3], dp[N-1][(firstColor+1)%3]+cost[N][(firstColor+2)%3]);

        min = Math.min(min, dp[N][(firstColor+1)%3]);
        min = Math.min(min, dp[N][(firstColor+2)%3]);
      }
      bw.write(min+"");
      bw.close();
  }
}
```
