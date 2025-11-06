```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.HashMap;
import java.util.HashSet;
import java.util.StringTokenizer;

public class Main { 
	
	static class City{
		int cost;
		int value;
		
		public City(int cost, int value) {
			this.cost = cost;
			this.value = value;
		}
	}
	static int[] dp;
	static City[] cities;
	static int goal,cityCnt,ans = Integer.MAX_VALUE;
	
    public static void main(String[] args) throws IOException {
    	init();
    	process();
    	print();
    }

    private static void init() throws IOException{
    	BufferedReader br = new BufferedReader(new InputStreamReader(System.in));;
    	StringTokenizer st = new StringTokenizer(br.readLine());
    	goal = Integer.parseInt(st.nextToken());
    	cityCnt = Integer.parseInt(st.nextToken());
    	dp = new int[1101];
    	cities = new City[cityCnt];
    	
    	Arrays.fill(dp, Integer.MAX_VALUE);
    	dp[0] = 0;
    	
    	
    	for (int i = 0; i < cityCnt; i++) {
    		st = new StringTokenizer(br.readLine());
    		int cost = Integer.parseInt(st.nextToken());
    		int value = Integer.parseInt(st.nextToken());
    		cities[i] = new City(cost,value);
    	}
    	
    	
    }
    
    private static void process() {
    	for (City c: cities) {
    		int cost = c.cost;
    		int value = c.value;
    		
    		for (int i = value; i <= 1100; i++) {
    			if (dp[i] > dp[i-value]+cost) {
    				dp[i] = dp[i-value]+cost;
    			}
    		}
    	}
    	
    	
    	for (int i = goal; i <= 1100; i++) {
    		ans = Math.min(ans, dp[i]);
    	}

    }
    

    
    private static void print() {
    	System.out.println(ans);
    }
}


```
