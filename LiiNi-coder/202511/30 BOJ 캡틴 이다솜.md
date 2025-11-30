```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        List<Integer> tetra = new ArrayList<>();
        for(int k=1; ; k++){
            // 총알 개수
            int t = k * (k + 1) * (k + 2) / 6;
            if(t > N)
                break;
            tetra.add(t);
        }
        int size = tetra.size();
        
        
        int[] dp = new int[N + 1];
        Arrays.fill(dp, Integer.MAX_VALUE);
        dp[0] = 0;
        for(int i = 0; i < size; i++){
            int t = tetra.get(i);
            for(int x = t; x <= N; x++){
                if(dp[x - t] != Integer.MAX_VALUE){
                    dp[x] = Math.min(dp[x], dp[x-t] + 1);
                }
            }
        }
        System.out.println(dp[N]);
    }
}

```
