```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.HashMap;
import java.util.HashSet;
import java.util.PriorityQueue;
import java.util.StringTokenizer;

public class Main {
	
	static BufferedReader br;
	static StringTokenizer st;
	static StringBuilder sb = new StringBuilder();
	
	static PriorityQueue<Integer> minQ = new PriorityQueue<>();
	static PriorityQueue<Integer> maxQ = new PriorityQueue<>(Collections.reverseOrder());
	
	static HashMap<Integer,Integer> map = new HashMap<>();
	
	static int size,len,qCnt;
	static int[][] arr,min,max;


	
    public static void main(String[] args) throws IOException {
    	init();
    	process();
    	print();
    }
    
    private static void init() throws IOException{
    	br = new BufferedReader(new InputStreamReader(System.in));
    	st = new StringTokenizer(br.readLine());
    	size = Integer.parseInt(st.nextToken());
    	len = Integer.parseInt(st.nextToken());
    	qCnt = Integer.parseInt(st.nextToken());
    	
    	arr = new int[size][size];
    	min = new int[size-len+1][size-len+1];
    	max = new int[size-len+1][size-len+1];
    	for (int i = 0; i < size; i++) {
    		st = new StringTokenizer(br.readLine());
    		for (int j = 0; j < size; j++) {
    			arr[i][j] = Integer.parseInt(st.nextToken());
    		}
    	}
    	
    	
    }
    
    private static void process() throws IOException {
    	getBase();
    	
    	for (int i = 0; i < size-len+1; i++) {

        	
        	if (i != 0)goUp(i);
        	PriorityQueue<Integer> preMinQ = new PriorityQueue<>();
        	PriorityQueue<Integer> preMaxQ = new PriorityQueue<>(Collections.reverseOrder());
        	HashMap<Integer,Integer> preMap = new HashMap<>();
        	preMinQ.addAll(minQ);
        	preMaxQ.addAll(maxQ);
        	preMap.putAll(map);
        	
    		calculate(i,0);
    		for (int j = 1; j < size-len+1; j++) {
    			goRight(i,j);
    			calculate(i,j);
    		}
    		
    		minQ = preMinQ;
    		maxQ = preMaxQ;
    		map = preMap;
    		
    	}
    	
    	for (int i = 0; i < qCnt; i++) {
    		st = new StringTokenizer(br.readLine());
    		int y = Integer.parseInt(st.nextToken())-1;
    		int x = Integer.parseInt(st.nextToken())-1;
    		sb.append(max[y][x] - min[y][x]).append("\n");
    	}
    	

    }
    
    private static void goUp(int y) {
    	for (int i = 0; i < len; i++) {
    		remove(y-1,i);
    	}
    	
    	for (int i = 0; i < len; i++) {
    		put(y+len-1,i);
    	}
    }
    
    private static void goRight(int y, int x) {
    	for (int i = y; i < y+len; i++) {
    		remove(i,x-1);
    		put(i,x+len-1);
    	}
    }
    

	

    private static void calculate(int y, int x) {
    	int minNum = minQ.peek();
    	int maxNum = maxQ.peek();
    	while(map.get(minNum) == 0) {
    		minQ.poll();
    		minNum = minQ.peek();
    	}
    	while(map.get(maxNum) == 0) {
    		maxQ.poll();
    		maxNum = maxQ.peek();
    	}
    	min[y][x] = minNum;
    	max[y][x] =maxNum;
    	
    }


    
    private static void getBase() {
    	for (int i = 0; i < len; i++) {
    		for (int j = 0; j < len; j++) {
    			put(i,j);
    		}
    	}
		
	}
    
    private static void put(int y,int x) {
    	int num  = arr[y][x];
    	if (map.containsKey(num) && map.get(num) > 0) {
    		map.replace(num, map.get(num)+1);
    	} else {
    		map.put(num, 1);
    		minQ.add(num);
    		maxQ.add(num);
    	}
    }
    
    private static void remove(int y,int x) {
    	int num = arr[y][x];
    	map.replace(num, map.get(num)-1);
    }

	private static void print() {
    	System.out.print(sb);
    }

}
```
