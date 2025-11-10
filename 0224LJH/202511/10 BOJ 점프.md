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
	
	static int[][] dp = new int[10001][500];
	static HashSet<Integer> set = new HashSet<>();
	static int total,setSize,ans;

	
    public static void main(String[] args) throws IOException {
    	init();
    	process();
    	print();

    	
    }
    
    private static void init() throws IOException{
    	BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    	StringTokenizer st = new StringTokenizer(br.readLine());
    	total = Integer.parseInt(st.nextToken());
    	setSize = Integer.parseInt(st.nextToken());
    	for (int i = 0; i < setSize; i++) {
    		set.add(Integer.parseInt(br.readLine()));
    	}
    	for (int i = 0; i <= 10000; i++) {
    		Arrays.fill(dp[i], Integer.MAX_VALUE);
    	}


    }
    
    private static void process() throws IOException {
    	if (set.contains(2)) {
    		ans = -1;
    		return;
    	}
    	dp[2][1] = 1;
    	for (int i = 2; i< total; i++) {
    		if (set.contains(i)) continue;
    		for (int j = 1; j < 500; j++) {
    			if (dp[i][j] == Integer.MAX_VALUE) continue;
    			
    			int more = j+1;
    			int less =j-1;
    			if (more < 500 && i+more <= total && !set.contains(i+more)) {
    				dp[i+more][more] = Math.min(dp[i+more][more], dp[i][j]+1);
    			}
    			if (j <  500 && i+j <= total && !set.contains(i+j)) {
    				dp[i+j][j] = Math.min(dp[i+j][j], dp[i][j]+1);
    			}
    			if (less != 0 && i+less <=total && !set.contains(i+less)) {
    				dp[i+less][less] = Math.min(dp[i+less][less], dp[i][j]+1);
    			}
    		}
    	}
    	
    	ans = Integer.MAX_VALUE;
    	for (int i = 1; i < 500; i++) {
    		ans = Math.min(ans, dp[total][i]);
    	}
    	if (ans == Integer.MAX_VALUE) ans = -1;

    }
    

	private static void print() {
    	System.out.print(ans);
    }

}
```
