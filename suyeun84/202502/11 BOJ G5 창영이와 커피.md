```java
import java.util.*;
import java.io.*;

class Solution
{
	public static void main(String[] args) throws Exception{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int N = Integer.parseInt(st.nextToken());
        int K = Integer.parseInt(st.nextToken());
        Integer[] coffee = new Integer[N];
        int[] dp = new int[K+1];
        Arrays.fill(dp, Integer.MAX_VALUE);
        dp[0] = 0;
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
        	coffee[i] = Integer.parseInt(st.nextToken());
        }

        for (int i = 0; i < N; i++) {
        	if (coffee[i] > K) continue;
        	dp[coffee[i]] = 1;
        	for (int j = K; j > coffee[i]; j--) {
        		if (dp[j - coffee[i]] != Integer.MAX_VALUE) {
                    dp[j] = Math.min(dp[j], dp[j - coffee[i]] + 1);
                }
        	}
        }
        
        if (dp[K] != Integer.MAX_VALUE) {
    		System.out.println(dp[K]);
    	} else {
    		System.out.println(-1);
    	}
	}
}

```
