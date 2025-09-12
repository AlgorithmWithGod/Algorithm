```java

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
	
	
	static int blockCnt;
	static long ans;
	static int[] blocks;
	static PriorityQueue<Block> pq = new PriorityQueue<>();
	static HashSet<Integer> nums = new HashSet<>();
	static PriorityQueue<Integer> numPq = new PriorityQueue<>();
	
	static class Block implements Comparable<Block>{
		int start;
		int height;
		
		public Block (int start, int height) {
			this.start = start;
			this.height = height;
		}
		
		@Override
		public int compareTo(Block b) {
			return Integer.compare(b.height, this.height);
		}
	}

    
    public static void main(String[] args) throws NumberFormatException, IOException {
		init();
		process();
		print();
    }
    
    public static void init() throws NumberFormatException, IOException {
    	BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    	blockCnt = Integer.parseInt(br.readLine());
    	blocks = new int[blockCnt];
    	ans = 0;
    	for (int i = 0; i < blockCnt; i++) {
    		blocks[i] = Integer.parseInt(br.readLine());
    		nums.add(blocks[i]);
    	}

    	
    }
    
    public static void process() { 	
    	ans = findLargest(0,blockCnt-1);
    	
    	
    }
    
    public static long findLargest(int start, int end) {
    	
    	if (start == end) return blocks[start];
    	
    	int mid = (start+end)/2;
    	long leftMax = findLargest(start,mid);
    	long rightMax = findLargest(mid+1,end);
    	long max = Math.max(leftMax, rightMax);
    	
    	int leftIdx = mid;
    	int rightIdx = mid+1;
    	long curNum = Math.min(blocks[leftIdx], blocks[rightIdx]);
    	long curMax =curNum*(rightIdx-leftIdx+1);
    	
    	while(true) {	
    		
    		if (leftIdx == start && rightIdx == end) break;
    		int nLeftNum = 0;
    		int nRightNum = 0;
    		if (start < leftIdx) nLeftNum = blocks[leftIdx-1];
    		if (rightIdx < end) nRightNum = blocks[rightIdx+1];
    		
    		if (nLeftNum <= nRightNum && rightIdx != end) {
    			rightIdx++;
    		} else {
    			leftIdx--;
    		}
    		
    		curNum = Math.min(curNum, blocks[rightIdx]);
    		curNum = Math.min(curNum, blocks[leftIdx]);
    		curMax = Math.max(curMax, curNum*(rightIdx-leftIdx+1));
    		
    	}
    	
    	max = Math.max(max, curMax);
    	
    	return max;
    }
    
    


    public static void print() {
    	System.out.println(ans);
    }
}
```
