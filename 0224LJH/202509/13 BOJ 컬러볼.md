```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
	
	static StringBuilder sb = new StringBuilder();
	
	static int ballCnt,sum;
	static int[] ans,numSum;
	static ArrayList<Ball>[] balls;
	
	static class Ball {
		int color;
		int idx;
		
		public Ball (int color, int idx){
			this.color = color;
			this.idx = idx;
		}
		
	}

    
    public static void main(String[] args) throws NumberFormatException, IOException {
      init();
      process();
      print();
    }
    
    @SuppressWarnings("unchecked")
	public static void init() throws NumberFormatException, IOException {
    	BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    	
    	ballCnt = Integer.parseInt(br.readLine());
    	ans = new int[ballCnt]; 
    	numSum = new int[ballCnt+1]; // i번 색상 공의 크기 합
    	balls = new ArrayList[2001];
    	
    	for (int i = 0 ; i <= 2000; i++) balls[i] = new ArrayList<>();
    	
    	for (int i = 0; i < ballCnt; i++) {
    		StringTokenizer st = new StringTokenizer(br.readLine());
    		int color = Integer.parseInt(st.nextToken());
    		int size = Integer.parseInt(st.nextToken());
    		Ball b = new Ball(color,i);
    		
    		balls[size].add(b);
    	}
    	
    	

    }
    
    public static void process() {   
    	for (int i = 1; i <= 2000; i++) {
    		ArrayList<Ball> tempBalls = balls[i]; 
    		
    		for (Ball b: tempBalls) {
    			ans[b.idx] = sum - numSum[b.color];
    		}
    		
    		for (Ball b: tempBalls) {
    			numSum[b.color] += i;
    		}
    		sum += tempBalls.size() * i;

    		
    	}


    	for (int i = 0; i < ballCnt; i++) {
    		sb.append(ans[i]).append("\n");
    	}
    }
    
    public static void print() {
    	System.out.println(sb.toString());
    }
}```
