```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

public class Main {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static int total,target,ans;
	static int[] points;
	static int[][] arr; 
	static boolean[] alive;
	
    public static void main(String[] args) throws IOException {

        init();
        process();
    	print();

    }
    
    private static void init() throws IOException{
    	total = Integer.parseInt(br.readLine());
    	points = new int[total];
    	alive = new boolean[total];
    	arr = new int[total][total];
    	ans = 0;
    	
    	Arrays.fill(alive, true);
    	
    	StringTokenizer st = new StringTokenizer(br.readLine());
    	for (int i = 0; i < total; i++) {
    		points[i] = Integer.parseInt(st.nextToken());
    	}
    	
    	for (int i = 0; i < total; i++) {
    		st = new StringTokenizer(br.readLine());
    		for (int j = 0; j < total; j++) {
    			arr[i][j] = Integer.parseInt(st.nextToken());
    		}
    	}
    	
    	target = Integer.parseInt(br.readLine());
    }
    
    private static void process() throws IOException {
    	
    	processDay(0,total);
    }
    
    private static void processDay(int nightCnt, int cnt) {
    	if (cnt%2 == 0) {
    		for (int i = 0; i < total; i++) {
    			if ( i != target && alive[i]) {
    				// 임의로 한명 죽임
    				alive[i] = false;
    				for (int j = 0; j < total; j++) {
    					points[j] += arr[i][j];
    				}
    				processDay(nightCnt+1,cnt-1);
    				
    				//원상복구
    				alive[i] = true;
    				for (int j = 0; j < total;j++) {
    					points[j] -= arr[i][j];
    				}
    				
    			}
    		}
    	} else {
    		if (cnt == 1) {
    			ans = Math.max(ans, nightCnt);
    			return;
    		}
    		
    		int highest = Integer.MIN_VALUE;
    		int highestIdx = -1;
    		for (int i = 0; i < total; i++) {
    			if (!alive[i]) continue;
    			if (points[i] > highest) {
    				highest = points[i];
    				highestIdx = i;
    			}
    		}
    		
    		if (highestIdx == target) {
    			ans = Math.max(ans, nightCnt);
    			return;
    		}
    		
			alive[highestIdx] = false;
			processDay(nightCnt,cnt-1);
			alive[highestIdx] = true;
    		
    	}
    	
    }
    

    
    

	private static void print() {
		System.out.println(ans);
    }

}
```
