```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.HashSet;
import java.util.StringTokenizer;

public class Main {
	
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static char[][] words;
	static int[][][] dp;
	static int ans = 0;
	
	
    public static void main(String[] args) throws IOException {

        init();
        process();
    	print();

    }
    
    private static void init() throws IOException{
    	words = new char[3][];
    	for (int i = 0; i < 3; i++) {
    		words[i] = br.readLine().toCharArray();
    	}
    	dp = new int[words[0].length+1][words[1].length+1][words[2].length+1];
    }
    
    private static void process() throws IOException {
    	for (int i = 1; i <= words[0].length; i++) {
    		for (int j = 1; j <= words[1].length; j++) {
    			for (int k = 1; k <= words[2].length; k++) {
    				if (words[0][i-1] == words[1][j-1] && words[1][j-1]  == words[2][k-1]) {
    					dp[i][j][k] = dp[i-1][j-1][k-1]+1;
    				} else {
    					dp[i][j][k] =Math.max(Math.max(dp[i-1][j][k], dp[i][j-1][k]), dp[i][j][k-1]);
    				}
    			}
    		}
    	}
    }
    
	private static void print() {
		System.out.println(dp[words[0].length][words[1].length][words[2].length]);
    }

}
```
