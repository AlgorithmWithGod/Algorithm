```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
	
	static int nodeCnt, sum,ans;
	static int[] arr;

    public static void main(String[] args) throws NumberFormatException, IOException {
    	init();
    	process();
    	print();
    	

    }
    
    public static void init() throws NumberFormatException, IOException {
    	BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    	nodeCnt = Integer.parseInt(br.readLine());
    	arr = new int[nodeCnt];
    	ans = 0;
    	for (int i = 0; i < nodeCnt; i++) {
    		arr[i] = Integer.parseInt(br.readLine());
    		sum += arr[i];
    	}

    }
    
    public static void process() { 	
    	int halfSum =sum/2;
    	int st = 0;
    	int end = 0;
    	
    	int curSum = arr[0];
    	
    	
    	while(true) {
    		ans = Math.max(ans,  Math.min(curSum, sum - curSum));
    		if (curSum <= halfSum) {
    			end++;
    			
    			if (end >= nodeCnt) break;
    			curSum += arr[end];
    		} else {
    			curSum -=arr[st];
    			st++;
    		}
    		
    	}

    }



	public static void print() {
		System.out.println(ans);
    }
}
```
