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
	
	static int ans,target;
	static HashSet<Integer> banSet = new HashSet<>();
	
    public static void main(String[] args) throws IOException {
    	init();
    	process();
    	print();
    }

    private static void init() throws IOException{
    	BufferedReader br = new BufferedReader(new InputStreamReader(System.in));;
    	target = Integer.parseInt(br.readLine());
    	
    	int banCnt = Integer.parseInt(br.readLine());
    	if (banCnt == 0) return;
    	StringTokenizer st = new StringTokenizer(br.readLine());
    	for (int i = 0; i < banCnt; i++) {
    		banSet.add(Integer.parseInt(st.nextToken()));
    	}
    }
    
    
    private static void process() {
    	ans = Math.abs(target - 100);
    	
    	for (int i = 0 ; i < 1000000; i++) {
    		int num = i;
    		int diff = Math.abs(target - num);
    		int len = String.valueOf(num).length();
    		boolean isPossible = true;
    		while(true) {
    			if (banSet.contains(num%10)) {
    				isPossible = false;
    				break;
    			}
    			
    			num /= 10;
    			if (num == 0) break;
    		}
    		
    		if (isPossible) ans = Math.min(ans, diff+len);
    	}
    }
    

    
    private static void print() {
    	System.out.println(ans);
    }
}


```
