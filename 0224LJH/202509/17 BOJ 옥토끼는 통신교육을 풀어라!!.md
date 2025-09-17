```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
	
	static int problemCnt;
	static Long ans;
	static long [] arr;
    
    public static void main(String[] args) throws NumberFormatException, IOException {
		init();
		process();
		print();
    }
    
    public static void init() throws NumberFormatException, IOException {
    	BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    	problemCnt = Integer.parseInt(br.readLine());
    	StringTokenizer st = new StringTokenizer(br.readLine());
    	ans = 1000_000_0000L;
    	arr = new long[problemCnt];
    	for (int i = 0; i < problemCnt; i++) {
    		arr[i] = Long.parseLong(st.nextToken());
    	}


    	
    }
    
    public static void process() { 	
    	Long st = 1L;
    	Long end = 1000_000_001L;
    	Long mid = (st+end)/2;
    	
    	while(st < end) {
    		boolean result = test(mid);
    		
    		if (result) {
    			ans = Math.min(ans, mid);
    			end = mid;
    		} else st = mid+1;
    		
    		mid = (st+end)/2;
    		
    	}
    }


	private static boolean test(Long diff) {
		long cnt = 0;
		
		for (int i = 0; i < problemCnt; i++) {
			long result = arr[i]/diff;
			if (arr[i]%diff ==0) result--;
			cnt += result;
		}
		
		if (cnt >= problemCnt) return false;


		return true;
	}

	public static void print() {
		System.out.println(ans);
    }
}
```
