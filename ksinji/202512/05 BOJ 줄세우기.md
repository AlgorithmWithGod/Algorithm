```java
import java.io.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());

        int[] arr = new int[n];
        int[] dp = new int[n];

        for (int i=0; i<n; i++){
            arr[i] = Integer.parseInt(br.readLine());
        }

        int lis = 0;
        for (int i=0; i<n; i++){
            dp[i] = 1;
            for (int j=0; j<i; j++){
                if (arr[j] < arr[i] && dp[j]+1>dp[i]){
                    dp[i] = dp[j]+1;
                    lis = Math.max(lis, dp[i]);
                }
            }
        }

        System.out.println(n-lis);
    }
}
```
