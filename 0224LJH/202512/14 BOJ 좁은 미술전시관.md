```java
import java.util.*;
import java.io.*;

public class Main {
	
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    
    static int size, closeCnt, ans;
    static int dp[][][];
    static int arr[][];

    public static void main(String[] args) throws IOException {
        while(true) {
        	init();
            if (size == 0 && closeCnt ==0) break;
            process();
            print();
        }

    }
    
    private static void init() throws IOException {
        
        StringTokenizer st = new StringTokenizer(br.readLine());
        size = Integer.parseInt(st.nextToken());
        closeCnt = Integer.parseInt(st.nextToken());
        ans = 0 ;
        if (size == 0 )return;
        
        dp = new int [size][3][closeCnt+1]; 
        // dp[i][j][k]: i번째칸까지 와서 k번만큼 방을 닫았을 때의  최댓값. 이때 j는 마지막에 어디를 닫았느냐를 의미 (0: 왼쪽, 1:오른쪽, 2:안닫음)
        arr = new int[size][2];
        
        
        for (int i = 0; i < size; i++) {
        	st = new StringTokenizer(br.readLine());
        	for (int j = 0; j < 2; j++) {
        		arr[i][j] = Integer.parseInt(st.nextToken());
        	}
        }
        
        

    }
    
    private static void process() {
    	if (closeCnt != 0) {
        	dp[0][0][1] = arr[0][1];
        	dp[0][1][1] = arr[0][0];
    	}

    	dp[0][2][0] = arr[0][1] + arr[0][0];
    	
    	for (int i = 1; i < size; i++) {
    		for (int j = 0; j <= closeCnt; j++) {
    			dp[i][2][j] = Math.max( Math.max(dp[i-1][0][j],dp[i-1][1][j] ), dp[i-1][2][j]);
    			if (dp[i][2][j] != 0) dp[i][2][j] += arr[i][0] + arr[i][1];
    			
    			if (j == 0) continue;
    			dp[i][1][j] = Math.max(dp[i-1][1][j-1],dp[i-1][2][j-1]);
    			if (dp[i][1][j] != 0) dp[i][1][j] += arr[i][0];
    			
    			dp[i][0][j] = Math.max(dp[i-1][0][j-1],dp[i-1][2][j-1]);
    			if (dp[i][0][j] != 0) dp[i][0][j] += arr[i][1];
    			
    		}
    	}
    	System.out.println(dp[size-1][0][closeCnt] + " " + dp[size-1][1][closeCnt] + " " + dp[size-1][2][closeCnt]);
    	ans = Math.max( Math.max(dp[size-1][0][closeCnt],dp[size-1][1][closeCnt]),dp[size-1][2][closeCnt]);

    }
    

    private static void print() {
        System.out.println(ans);
    }
}
```
