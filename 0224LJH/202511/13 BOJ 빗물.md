```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.HashMap;
import java.util.HashSet;
import java.util.LinkedList;
import java.util.PriorityQueue;
import java.util.Queue;
import java.util.StringTokenizer;

public class Main {
	
	static int height, width,ans;
	static boolean[][] arr;

	
    public static void main(String[] args) throws IOException {
    	init();
    	process();
    	print();

    	
    }
    
    private static void init() throws IOException{
    	BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    	StringTokenizer st = new StringTokenizer(br.readLine());
    	
    	height = Integer.parseInt(st.nextToken());
    	width = Integer.parseInt(st.nextToken());
    	
    	arr = new boolean[height][width];
    	ans = 0;
    	
    	st = new StringTokenizer(br.readLine());
    	for (int i = 0; i < width; i++) {
    		int h = Integer.parseInt(st.nextToken());
    		for (int j = 0; j < j; j++) {
    			arr[j][i]= true;
    		}
    	}



    }
    
    private static void process() throws IOException {
    	for (int i = 0; i < height; i++) {
    		ArrayList<Integer> idxes = new ArrayList<>();
    		for (int j = 0; j < width; j++) {
    			if(arr[i][j]) idxes.add(j);
    		}
    		
    		if (idxes.size() < 2) return;
    		
    		int pre = idxes.get(0);
    		
    		for(int j = 1; j < idxes.size(); j++) {
    			int cur = idxes.get(i);
    			ans += cur - pre;
    			pre = cur;
    		}
    	}

    }
    

	private static void print() {
    	System.out.print(ans);
    }

}
```
