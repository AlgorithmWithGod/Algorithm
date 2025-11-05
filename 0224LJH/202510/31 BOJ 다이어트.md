```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;

public class Main { 
	
	static long diff;
	static StringBuilder sb = new StringBuilder();
	
	
    public static void main(String[] args) throws IOException {
    	init();
    	process();
    	print();
    }

    private static void init() throws IOException{
    	BufferedReader br = new BufferedReader(new InputStreamReader(System.in));;
    	diff = Integer.parseInt(br.readLine());
    }
    
    private static void process() {
    	
    	long pre =1l;
        boolean isEmpty = true;
    	for (long i = 2; i <= 500000; i++) {
    		long num = i*i;
    		if (num - pre > diff) break;
    		pre = num;
    		
    		long target = num - diff;
    		if (target == 0) continue;
    		long sqrt = (long) Math.sqrt(target);
    		if (sqrt*sqrt != target) continue;
    		isEmpty = false;
    		sb.append(i).append("\n");
    		
    		
    		
    	}
    	
    	if(isEmpty)sb.append("-1");

    }
    

    
    private static void print() {
    	System.out.println(sb.toString());
    }
}


```
