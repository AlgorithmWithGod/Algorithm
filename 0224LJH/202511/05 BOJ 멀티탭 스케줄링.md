```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.HashSet;
import java.util.StringTokenizer;

public class Main { 
	
	static int size,totalLen,count;
	static int[] arr;
	static HashSet<Integer> set = new HashSet<>();
	
    public static void main(String[] args) throws IOException {
    	init();
    	process();
    	print();
    }

    private static void init() throws IOException{
    	BufferedReader br = new BufferedReader(new InputStreamReader(System.in));;
    	StringTokenizer st = new StringTokenizer(br.readLine());
    	//이거 그냥 lfd 라는 페이지 교체 알고리즘을 쓰면 된다!
    	size = Integer.parseInt(st.nextToken());
    	totalLen = Integer.parseInt(st.nextToken());
    	arr = new int[totalLen];
    	
    	st = new StringTokenizer(br.readLine());
    	for (int i = 0; i <totalLen; i++) {
    		arr[i] = Integer.parseInt(st.nextToken());
    	}

    	
    }
    
    private static void process() {
    	count = 0;

    	
    	for (int i = 0; i < totalLen; i++) {
    		if (set.size() < size) {
    			set.add(arr[i]);
    			continue;
    		}
    		if (set.contains(arr[i])) continue;
    		
    		int target = -1;
    		int targetDistance = 0;
    		for (int num: set) {
    			int distance = 10000;
    			for (int j = i; j < totalLen; j++) {
    				if (arr[j] == num) {
    					distance = j-i;
    					break;
    				}
    			}
    			if (targetDistance < distance) {
    				target = num;
    				targetDistance = distance;
    			}
    		}
    		
    		count++;
    		set.remove(target);
    		set.add(arr[i]);
    		
    	}


    }
    

    
    private static void print() {
    	System.out.println(count);
    }
}


```
