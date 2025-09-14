```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
	
	static StringBuilder sb = new StringBuilder();
	static long size, oneMax,twoMax,threeMax,ans;
	static Long[] num;
	
    
    public static void main(String[] args) throws NumberFormatException, IOException {
      init();
      process();
      print();
    }

	public static void init() throws NumberFormatException, IOException {
    	BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    	size = Integer.parseInt(br.readLine());
    	num = new Long[6];
    	StringTokenizer st = new StringTokenizer(br.readLine());
    	for (int i = 0 ; i < 6 ; i++) {
    		num[i] = Long.parseLong(st.nextToken());
    	}
    	

    }
    
    public static void process() {   

    	
    	getOneMax();
    	getTwoMax();
    	getThreeMax();
    	
//    	System.out.println(oneMax);
//    	System.out.println(twoMax);
//    	System.out.println(threeMax);
//    	
    	ans = 0;
    	
    	if (size == 1) {
    		long max = 0;
    		for (int i = 0; i < 6; i++) {
    			max = Math.max(max, num[i]);
    			ans += num[i];
    		}
    		ans -= max;
    		return;
    	}
    	ans += ((size-2) * (size-1) * 4 + (size-2) * (size-2)) * oneMax;
    	ans += ((size-1)*4 + (size-2)*4)* twoMax;
    	ans += 4 * threeMax;
    	
    }
    
    private static void getThreeMax() {
    	threeMax = Long.MAX_VALUE;
		for (int i = 0; i < 6; i++) {
			for (int j = i+1; j < 6; j++) {
				for (int k = j+1; k < 6; k++) {
					Long n1 = num[i];
					Long n2 = num[j];
					Long n3 = num[k];
					
					if (i + j == 5 || i + k == 5 || j + k == 5) continue;
					
					threeMax = Math.min(threeMax, n1+n2+n3);
				}
			}
		}
		
	}

	private static void getTwoMax() {
		twoMax = Long.MAX_VALUE;
		for (int i = 0; i < 6; i++) {
			for (int j = i+1; j < 6; j++) {
				Long n1 = num[i];
				Long n2 = num[j];
				
				if (i + j == 5) continue;
				
				twoMax = Math.min(twoMax, n1+n2);
			}
		}	
		
	}

	private static void getOneMax() {
		Long temp = Long.MAX_VALUE;
		for (int i = 0 ; i < 6; i++) {
			temp = Math.min(temp, num[i]);
		}
		oneMax = temp;
	}

	public static void print() {
    	System.out.println(ans);
    }
}
```
