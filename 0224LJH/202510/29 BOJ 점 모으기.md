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
	
	static int size, pointCnt,xIdx,yIdx;
	static int[] xArr,yArr;
	static long xSum, ySum,xCumul,yCumul, ansX, ansY;
	
	
    public static void main(String[] args) throws IOException {
    	init();
    	process();
    	print();
    }

    private static void init() throws IOException{
    	BufferedReader br = new BufferedReader(new InputStreamReader(System.in));;
    	StringTokenizer st = new StringTokenizer(br.readLine());
    	size = Integer.parseInt(st.nextToken());
    	pointCnt = Integer.parseInt(st.nextToken());
    	xIdx = 0;
    	yIdx = 0;
    	xSum = 0;
    	ySum = 0;
    	ansX = Long.MAX_VALUE;
    	ansY = Long.MAX_VALUE;
    	
    	xArr = new int[pointCnt];
    	yArr = new int[pointCnt];
    	
    	xCumul = 0;
    	yCumul = 0;
    	for (int i = 0; i < pointCnt; i++) {
    		st = new StringTokenizer(br.readLine());
    		int y = Integer.parseInt(st.nextToken());
    		int x = Integer.parseInt(st.nextToken());
    		xSum += x;
    		ySum += y;
    		xArr[i] = x;
    		yArr[i] = y;
    	}


    }
    
    private static void process() {
    	Arrays.sort(xArr);
    	Arrays.sort(yArr);
    	
    	int num = 1;
    	while(num <= size) {
    		long curSumX = 0;
    		long curSumY = 0;
    		while (xIdx < pointCnt && num >= xArr[xIdx]) {
    			xCumul += xArr[xIdx++];
    		}
    		while (yIdx < pointCnt && num >= yArr[yIdx]) {
    			yCumul += yArr[yIdx++];
    		}

    		curSumX = num*xIdx - xCumul*2 + xSum - num * (pointCnt - xIdx);
    		curSumY = num*yIdx - yCumul*2 + ySum - num * (pointCnt - yIdx);
    		
    		ansX = Math.min(ansX, curSumX);
    		ansY = Math.min(ansY, curSumY);
    		num++;
    	}
    }
    

    
    private static void print() {
    	System.out.println(ansY + ansX);
    }
}


```
