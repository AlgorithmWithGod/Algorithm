```java

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.HashSet;
import java.util.List;
import java.util.StringTokenizer;

public class Main {
	
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static int target, cnt;
	static long[][] dp;
	
    public static void main(String[] args) throws IOException {
    	init();
    	process();
    	print();

    }
    
    private static void init() throws IOException{
    	StringTokenizer st = new StringTokenizer(br.readLine());
    	target = Integer.parseInt(st.nextToken());
    	cnt = Integer.parseInt(st.nextToken());
    	dp = new long[target+1][cnt+1];
    }
    
    private static void process() throws IOException {
    	dp[0][0] = 1;
    	for (int i = 0; i <= target; i++) {
    		for (int j = 0; j <= target; j++) {
    			if (i+j > target) break;
    			for (int k = 1; k <= cnt; k++) {
    				dp[i+j][k] += dp[i][k-1];
    				dp[i+j][k] %= 1000_000_000;
    			}
    		}
    	}
    	
    	
    }

    
	private static void print() {
		System.out.println(dp[target][cnt]);
    }

}
```
