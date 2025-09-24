```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static StringBuilder sb = new StringBuilder();
    static int N,M,H;
    static List<Integer>[] blocks;

    public static void main(String[] args) throws Exception {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        H = Integer.parseInt(st.nextToken());

        blocks = new List[N+1];
        for (int i = 1; i <= N; i++) {
            blocks[i] = new ArrayList<>(M+1);
        }

        for (int i = 1; i <= N; i++) {
            st = new StringTokenizer(br.readLine());
            while(st.hasMoreTokens()){
                blocks[i].add(Integer.parseInt(st.nextToken()));
            }
            blocks[i].add(0); //블록 안 쌓는 경우 고려
        }

        int[][] dp = new int[N+1][H+1];//dp[i][j] = i번째 학생까지 고려했을때, j 높이를 쌓는 경우의 수
        dp[0][0] = 1;

        for (int i = 1; i <= N; i++) {
            for (int j = 0; j <= H; j++) {
                for (int cur : blocks[i]) {
                    if(cur <= j){
                        dp[i][j] += dp[i-1][j-cur];
                        dp[i][j] %= 10007;
                    }       
                }
            }
        }
        bw.write(dp[N][H] + "");
        bw.close();
    }
    
}
```
