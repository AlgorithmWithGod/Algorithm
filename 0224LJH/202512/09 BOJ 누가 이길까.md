```java

import java.util.StringTokenizer;
import java.util.*;
import java.io.*;

public class Main {
	
	static int[] total = new int[2];
	static long[][] people = new long[2][100001];
	static long[][] cumul = new long[2][100001];
	static long win,lose,draw;

    public static void main(String[] args) throws IOException {
    	init();
    	process();
    	print();

    }
    
    private static void init() throws IOException{
    	BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    	StringTokenizer st = new StringTokenizer(br.readLine());
    	total[0] = Integer.parseInt(st.nextToken());
    	total[1] = Integer.parseInt(st.nextToken());
    	win = 0;
    	lose = 0;
    	draw = 0;
    	
    	for (int i = 0 ; i < 2; i++) {
        	st = new StringTokenizer(br.readLine());
        	
        	for (int j = 0; j < total[i]; j++) {
        		int num = Integer.parseInt(st.nextToken());
        		people[i][num]++;
        	}
    	}
    	
   
    
    }
    
    private static void process() throws IOException {
    	for (int i = 1; i<= 100000; i++) {
    		for (int j = 0; j < 2; j++) {
    			cumul[j][i] = cumul[j][i-1] + people[j][i];
    		}
    	}
    	
    	for (int i = 1; i <= 100000; i++) {
    		win += people[0][i] * (cumul[1][i-1]);
    		lose += people[1][i] * (cumul[0][i-1]);
    		draw += people[0][i] * people[1][i];
    	}
    	
    	
    }
    
   private static void print() {
      System.out.println(win + " "+ lose +" " + draw);
    }

}
```
