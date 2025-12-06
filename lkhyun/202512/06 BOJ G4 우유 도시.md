```java
import java.util.*;
import java.io.*;

public class Main{
    static class State{
        int lastMilk;
        int cnt;
        State(int lastMilk,int cnt){
            this.lastMilk = lastMilk;
            this.cnt = cnt;
        }
    }
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static StringBuilder sb = new StringBuilder();
    static int N;
    static int[][] stores;
    static State[][] dp;

    public static void main(String[] args) throws Exception {
        N = Integer.parseInt(br.readLine());
        stores = new int[N+1][N+1];
        
        for(int i = 1; i<=N; i++){
            st = new StringTokenizer(br.readLine());
            for(int j = 1; j <= N; j++){
                stores[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        dp = new State[N+1][N+1];
        
        if(stores[1][1] == 0){
            dp[1][1] = new State(0, 1);
        }else{
            dp[1][1] = new State(-1, 0);
        }
        

        for(int j = 2; j <= N; j++){
            int nextMilk = (dp[1][j-1].lastMilk + 1) % 3;
            if(dp[1][j-1].lastMilk == -1) nextMilk = 0;
            
            if(stores[1][j] == nextMilk){
                dp[1][j] = new State(stores[1][j], dp[1][j-1].cnt + 1);
            }else{
                dp[1][j] = new State(dp[1][j-1].lastMilk, dp[1][j-1].cnt);
            }
        }
        
        for(int i = 2; i <= N; i++){
            int nextMilk = (dp[i-1][1].lastMilk + 1) % 3;
            if(dp[i-1][1].lastMilk == -1) nextMilk = 0;
            
            if(stores[i][1] == nextMilk){
                dp[i][1] = new State(stores[i][1], dp[i-1][1].cnt + 1);
            }else{
                dp[i][1] = new State(dp[i-1][1].lastMilk, dp[i-1][1].cnt);
            }
        }
        
        for(int i = 2; i<=N;i++){
            for(int j = 2; j<=N; j++){
                State up = dp[i-1][j];
                State left = dp[i][j-1];
                
                int upNextMilk = (up.lastMilk + 1) % 3;
                if(up.lastMilk == -1) upNextMilk = 0;
                
                int leftNextMilk = (left.lastMilk + 1) % 3;
                if(left.lastMilk == -1) leftNextMilk = 0;
                
                int upCnt = up.cnt + (stores[i][j] == upNextMilk ? 1 : 0);
                int leftCnt = left.cnt + (stores[i][j] == leftNextMilk ? 1 : 0);
                
                if(upCnt >= leftCnt){
                    if(stores[i][j] == upNextMilk){
                        dp[i][j] = new State(stores[i][j], upCnt);
                    }else{
                        dp[i][j] = new State(up.lastMilk, upCnt);
                    }
                }else{
                    if(stores[i][j] == leftNextMilk){
                        dp[i][j] = new State(stores[i][j], leftCnt);
                    }else{
                        dp[i][j] = new State(left.lastMilk, leftCnt);
                    }
                }
            }
        }
        bw.write(dp[N][N].cnt+"");
        bw.close();
    }
}
```
