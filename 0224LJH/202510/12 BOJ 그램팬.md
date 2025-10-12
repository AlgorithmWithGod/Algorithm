```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
	
	static final char START = 'A';
	static final char FINAL = 'Z';
	static String input;
	static long ans;
    
    public static void main(String[] args) throws NumberFormatException, IOException {
    	init();
    	process();
    	print();
    }
    

    
    public static void init() throws NumberFormatException, IOException {
    	BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    	input = br.readLine();
	}
    
    public static void process() throws IOException { 	
    	int idx = 0;
    	int size = input.length();
    	long cnt = 0;
    	long serialStart = 0;
    	
    	while(idx < size -1 ){
    		if (input.charAt(idx) == START) {
    			serialStart++;
    			idx++;
    		}
    		else if (input.charAt(idx) == START + 1 && serialStart != 0) {
    			boolean isGramPen = false;
    			char target = 'B';
    			long serialLast = 1;
    			
    			
    			while(idx < size) {
    				if (input.charAt(idx) == target) {
    					if (target == 'Z') serialLast++;
    					
    				} else if(target != 'Z' && input.charAt(idx) == target+1) {
    					target++;
    					if (target == 'Z') isGramPen = true;
    				} else {
    					break;
    				}
    				idx++;
    			}
    			
    			if (isGramPen) cnt += serialStart*serialLast;
    			serialStart = 0;
    		} else {
    			idx++;
    			serialStart = 0;
    		}
    		
    	}
    	ans = cnt;
    }
    



	public static void print() {
		System.out.print(ans);

    }
}
```
