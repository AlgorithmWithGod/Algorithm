```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args)throws IOException {
        BufferedReader br= new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st= new StringTokenizer(br.readLine());
        int D=Integer.parseInt(st.nextToken());
        int P=Integer.parseInt(st.nextToken());
        int[][] pipe = new int[P][2];
        for(int i=0; i<P;i++){
            st = new StringTokenizer(br.readLine());
            pipe[i][0]=Integer.parseInt(st.nextToken());
            pipe[i][1]=Integer.parseInt(st.nextToken());
        }
        int[] dp=new int[D+1];
        int INF= Integer.MAX_VALUE;
        dp[0]=INF;

        for(int i = 0; i<P; i++){
            int l = pipe[i][0];
            int c = pipe[i][1];
            for(int j = D; j>=l; j--){
                if(dp[j-l]<=0){
                    continue;
                }
                dp[j] = Math.max(dp[j], Math.min(dp[j-l], c));
            }
        }
        System.out.println(dp[D]);
    }
}

```
