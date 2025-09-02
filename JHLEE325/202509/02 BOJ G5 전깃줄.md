```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int n = Integer.parseInt(br.readLine());
        int[][] elec = new int[n][2];
        int[] dp = new int[n];

        for(int i=0;i<n;i++){
            st = new StringTokenizer(br.readLine());
            elec[i][0]= Integer.parseInt(st.nextToken());
            elec[i][1] = Integer.parseInt(st.nextToken());
        }

        Arrays.sort(elec,(o1,o2)->{
            return o1[0]-o2[0];
        });

        for(int i=0;i<n;i++){
            dp[i]=1;

            for(int j=0;j<i;j++){
                if(elec[i][1]>elec[j][1]){
                    dp[i] = Math.max(dp[i],dp[j]+1);
                }
            }
        }

        int result = 0;
        for(int i=0;i<n;i++){
            if(result<dp[i]){
                result=dp[i];
            }
        }

        System.out.println(n-result);
    }
}

```
