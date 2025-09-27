```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

class Main {
	
	static int bookCnt, bookMax, plusMax, minusMax,ans;
	static PriorityQueue<Integer> plusPq = new PriorityQueue<>(Collections.reverseOrder());
	static PriorityQueue<Integer> minusPq = new PriorityQueue<>(Collections.reverseOrder());
    
    public static void main(String[] args) throws NumberFormatException, IOException {
       init();
       process();
       print();

    }

    
    public static void init() throws NumberFormatException, IOException {
    	BufferedReader br= new BufferedReader(new InputStreamReader(System.in));
    	StringTokenizer st = new StringTokenizer(br.readLine());
    	
    	bookCnt = Integer.parseInt(st.nextToken());
    	bookMax = Integer.parseInt(st.nextToken());
    	plusMax = 0;
    	minusMax = 0;
    	st = new StringTokenizer(br.readLine());
    	
    	for (int i = 0; i < bookCnt; i++) {
    		int num = Integer.parseInt(st.nextToken());
    		if (num < 0 ) {
    			num *= -1;
    			minusPq.add(num);
    			minusMax = Math.max(minusMax, num);
    		} else {
    			plusPq.add(num);
    			plusMax = Math.max(plusMax, num);
    		}
    	}

    }
    
    public static void process() throws IOException {   
    	ans = 0;
    	
    	while (!minusPq.isEmpty()) {
    		ans += minusPq.peek();
    		for (int i = 0; i < bookMax; i++) {
    			if (minusPq.isEmpty()) break;
    			minusPq.poll();
    		}
    		
    	}
    	while (!plusPq.isEmpty()) {
    		ans += plusPq.peek();
    		for (int i = 0; i < bookMax; i++) {
    			if (plusPq.isEmpty()) break;
    			plusPq.poll();
    		}
    		
    	}
    	
    	ans *= 2;
    	ans -= Math.max(minusMax, plusMax);

    }
    

   public static void print() {
      System.out.println(ans);
    }
}
```
