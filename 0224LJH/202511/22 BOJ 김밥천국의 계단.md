```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.HashMap;
import java.util.HashSet;
import java.util.LinkedList;
import java.util.PriorityQueue;
import java.util.Queue;
import java.util.StringTokenizer;

public class Main {
	
	static int[] dp = new int[1000_001];
	static int target, totalJump;
	static String ans = "water";
	
    public static void main(String[] args) throws IOException {
    	init();
    	process();
    	print();
    }
    
    private static void init() throws IOException{
    	BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    	StringTokenizer st = new StringTokenizer(br.readLine());
    	target = Integer.parseInt(st.nextToken());
    	totalJump = Integer.parseInt(st.nextToken());
    	Arrays.fill(dp, Integer.MAX_VALUE);
    	dp[0] = 0;
    }
    
    private static void process() throws IOException {
    	for (int i = 0; i < 1000_000; i++) {
    		int next = i+1;
    		int jump = i + i/2;
    		dp[next] = Math.min(dp[next], dp[i]+1);
    		if (jump <= 1000000) dp[jump] = Math.min(dp[jump], dp[i]+1);
    	}
    	
    	if (dp[target] <= totalJump) ans = "minigimbob";
    }
    
    

	private static void print() {
		System.out.println(ans);
    }

}
```
