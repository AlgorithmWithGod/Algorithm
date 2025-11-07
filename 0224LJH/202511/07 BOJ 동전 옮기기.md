```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.HashMap;
import java.util.HashSet;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;

public class Main { 
	
	static int len,idx1,idx2;
	static boolean[][] dp;
	static char[] arr,comp,move = new char[2];
	static char last = '1';
	static String ans;
	static Queue<Character> arrQ = new LinkedList<>();
	static Queue<Character> fingerQ = new LinkedList<>();
	
    public static void main(String[] args) throws IOException {
    	init();
    	process();
    	print();
    }

    private static void init() throws IOException{
    	BufferedReader br = new BufferedReader(new InputStreamReader(System.in));;
    	len = Integer.parseInt(br.readLine());
    	char[] temp = br.readLine().toCharArray();
    	arr = br.readLine().toCharArray();
    	
    	StringTokenizer st = new StringTokenizer(br.readLine());
    	idx1 = Integer.parseInt(st.nextToken());
    	idx2 = Integer.parseInt(st.nextToken());
    	
    	int idx = 0;
    	int moveIdx = 0;
    	
    	comp = new char[len-2];
    	
    	for (int i = 0; i < len; i++) {
    		if (i == idx1 || i == idx2) {
    			move[moveIdx++] = temp[i];
    		} else {
    			comp[idx++] =temp[i];
    		}
    		
    	}
    	dp = new boolean[len][3]; // dp[i][j] move j개쓰고 이곳에 도달가능?

    	
    }
    
    
    private static void process() {
    	int idx = 0;
    	int mIdx = 0;
    	
    	
    	if (arr[0] != comp[0] && arr[0] != move[0]) {
    		ans = "NO";
    		return;
    	}
    	
    	if (arr[0] == comp[0]) {
    		dp[0][0] = true;
    	}
    	if (arr[0] == move[0]) {
    		dp[0][1] = true;
    	}
    	
    	
    	for (int i = 1; i < len; i++) {
    		for (int j = 0; j < 3; j++) {
    			
    			if (!dp[i-1][j]) continue;
    			// 이제 비교
    			
    			if (i-j < len-2) {
        			if (arr[i] == comp[i-j]) {
        				dp[i][j] = true;
        			} 
    			}

    			if (j!= 2 && arr[i] == move[j]) {
    				dp[i][j+1] = true;
    			}
    		}
    	}
    	
    	ans = dp[len-1][2]?"YES":"NO";
    }
    

    
    private static void print() {
    	System.out.println(ans);
    }
}


```
