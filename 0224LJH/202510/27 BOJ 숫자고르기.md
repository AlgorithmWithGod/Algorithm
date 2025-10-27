```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.HashSet;
import java.util.PriorityQueue;
import java.util.StringTokenizer;

public class Main {
	static StringBuilder sb = new StringBuilder();
	static int totalNum,left;
	static int[] arr,numCnt;
	static boolean[] isDead;

    public static void main(String[] args) throws IOException {
        init();
        process();
        print();
    }

    private static void init() throws IOException{
    	BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    	totalNum = Integer.parseInt(br.readLine());
    	left= totalNum;
    	arr = new int[totalNum+1];
    	numCnt = new int[totalNum+1];
    	isDead = new boolean[totalNum+1];
    	
    	for (int i = 1; i <= totalNum; i++) {
    		arr[i] = Integer.parseInt(br.readLine());
    		numCnt[arr[i]]++;
    	}
    }
    
    private static void process() {
    	boolean isEnd = false;
    	while(!isEnd) {
    		isEnd = true;
    		for (int i = 1; i <= totalNum; i++) {
    			if (isDead[i]) continue;
    			if (numCnt[i] == 0) {
    				numCnt[arr[i]]--;
    				isEnd = false;
    				left--;
    				isDead[i] = true;
    			}
    		}
    	}
    	
    	sb.append(left);
    	for (int i = 1; i<= totalNum; i++) {
    		if(!isDead[i]) sb.append("\n").append(i);
    	}
    	
    }
    

    
    private static void print() {
    	System.out.println(sb.toString());
    }
}


```
