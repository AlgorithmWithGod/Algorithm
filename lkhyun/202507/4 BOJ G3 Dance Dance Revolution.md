```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int[][][] dp; //dp[현재 명령][왼발][오른발] = 드는 힘
    public static void main(String[] args) throws Exception{
        st = new StringTokenizer(br.readLine());
        int N = st.countTokens();

        dp = new int[N][5][5];
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < 5; j++) {
                Arrays.fill(dp[i][j], Integer.MAX_VALUE);
            }
        }
        dp[0][0][0] = 0;

        for (int i = 1; i < N; i++) {
            int cur = Integer.parseInt(st.nextToken());
            for (int j = 0; j < 5; j++) {
                for (int k = 0; k < 5; k++) {
                    if(dp[i-1][j][k] != Integer.MAX_VALUE) {
                        if(j == 0){
                            dp[i][cur][k] = Math.min(dp[i][cur][k],dp[i-1][j][k] + 2);
                        }else{
                            int jDiff = Math.abs(cur - j);
                            if(jDiff == 0){ //같은 위치
                                dp[i][cur][k] = Math.min(dp[i][cur][k], dp[i-1][j][k] + 1);
                            }else if(jDiff % 2 == 1) { //인접한 경우
                                dp[i][cur][k] = Math.min(dp[i][cur][k], dp[i-1][j][k] + 3);
                            }else{// 반대 경우
                                dp[i][cur][k] = Math.min(dp[i][cur][k], dp[i-1][j][k] + 4);
                            }
                        }
                        if(k == 0){
                            dp[i][j][cur] = Math.min(dp[i][j][cur],dp[i-1][j][k] + 2);
                        }else{
                            int kDiff = Math.abs(cur - k);
                            if(kDiff == 0){ //같은 위치
                                dp[i][j][cur] = Math.min(dp[i][j][cur], dp[i-1][j][k] + 1);
                            }else if(kDiff % 2 == 1) { //인접한 경우
                                dp[i][j][cur] = Math.min(dp[i][j][cur], dp[i-1][j][k] + 3);
                            }else{// 반대 경우
                                dp[i][j][cur] = Math.min(dp[i][j][cur], dp[i-1][j][k] + 4);
                            }
                        }
                    }
                }
            }
        }
        int ans = Integer.MAX_VALUE;
        for (int i = 0; i < 5; i++) {
            for (int j = 0; j < 5; j++) {
                ans = Math.min(ans, dp[N-1][i][j]);
            }
        }
        bw.write(ans+"");
        bw.close();
    }
}
```
