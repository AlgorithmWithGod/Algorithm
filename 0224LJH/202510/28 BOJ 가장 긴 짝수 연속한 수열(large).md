```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {

	
	static int len,totalErase,curErase,start,end,ans,curLen;
	static int[] arr;
	
    public static void main(String[] args) throws IOException {
    	init();
    	process();
    	print();
    }

    private static void init() throws IOException{
    	BufferedReader br = new BufferedReader(new InputStreamReader(System.in));;
    	StringTokenizer st = new StringTokenizer(br.readLine());
    	len = Integer.parseInt(st.nextToken());
    	totalErase = Integer.parseInt(st.nextToken());
    	arr = new int[len];
    	st = new StringTokenizer(br.readLine());
    	for (int i = 0; i < len; i++) {
    		arr[i] = Integer.parseInt(st.nextToken());
    	}
    	
    	start = 0;
    	end = 0;
    	ans = 0;
    	curErase = 0;
    	curLen = 0;

    }
    
    private static void process() {
    	if (arr[0] %2 == 0) {
    		curLen++;
    		ans++;
    	} else {
    		curErase++;
    	}

    	while( end < len) {
    		if (curErase < totalErase) {
    			end++;
    			if (end == len)break;
    			if (arr[end] %2 == 0) curLen++;
    			else curErase++;
    			
    		} else if (curErase == totalErase && end + 1 < len && arr[end+1]%2 ==0) {
    			end++;
    			curLen++;
    		} else {
    			if (arr[start] %2 == 0) {
    				curLen--;
    			} else {
    				curErase--;
    			}
    			start++;
    		}
    		
    		
    		
    		ans = Math.max(ans, curLen);
    	}
    }
    

    
    private static void print() {
    	System.out.println(ans);
    }
}


```
