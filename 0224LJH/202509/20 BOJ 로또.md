```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
	
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	
	static int[] arr;
	static long[][] dp;
	static int numCnt, max; 
	static long ans;

    public static void main(String[] args) throws NumberFormatException, IOException {
    	int TC = Integer.parseInt(br.readLine());
    	for (int tc =1; tc <= TC; tc++) {
    		init();
    		process();
    		print();
    	}

    }
    
    public static void init() throws NumberFormatException, IOException {
    	StringTokenizer st = new StringTokenizer(br.readLine());
    	numCnt = Integer.parseInt(st.nextToken());
    	max = Integer.parseInt(st.nextToken());
    	arr = new int[numCnt];
    	dp = new long[numCnt][max+1];
    	ans = 0;
    }
    
    public static void process() { 	
    	Arrays.fill(dp[numCnt-1], 1);
    	for (int i = numCnt-1; i > 0; i--) {
    		for (int j = max; j >=0; j--) {
    			dp[i-1][j/2] += dp[i][j];
    		}
    		for (int j = max; j > 0; j--) {
    			dp[i-1][j-1] += dp[i-1][j];
    		}
    	}
    	
    	for (int i = 0; i < numCnt; i++) {
    		for (int j = 0; j <= max; j++) {
    			System.out.print (dp[i][j]+ " ");
    		}
    		System.out.println();
    	}
    	for (int i = 1; i <= max; i++) {
    		
    		ans += dp[0][i];
    	}

    }



	public static void print() {
		System.out.println(ans);
    }
}
```
