```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N,X;
    static int[] pipeLen;
    static int[] pipeCnt;
    static int[] dp; // dp[i] = 길이 i를 만드는 방법의 수

    public static void main(String[] args) throws Exception {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        X = Integer.parseInt(st.nextToken());

        pipeLen = new int[N];
        pipeCnt = new int[N];
        dp = new int[X+1];
        
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            pipeLen[i] = Integer.parseInt(st.nextToken());
            pipeCnt[i] = Integer.parseInt(st.nextToken()); 
        }

        dp[0] = 1;
        for (int i = 0; i < N; i++) { //모든 파이프에 대하여
            for (int j = X; j >= 0; j--) { //길이를 고려
                for (int k = 1; k <= pipeCnt[i]; k++) {
                    if(j - pipeLen[i]*k >= 0){
                        dp[j] += dp[j-pipeLen[i]*k];
                    }
                }
            }
        }
        bw.write(dp[X]+"");
        bw.close();
    }
}
```
