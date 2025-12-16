```java
import java.util.*;
import java.io.*;

public class Main {
	/*
	 * R도, C도 아래의 조건이 성립해야함
	 * S초일때, 대상의 좌표를 N^(1~s)로 나누었을때, 나머지가 ( (N-K)/2~ (N+k)/2 -1 ) * N^(0~s-1)에 포함되면 됨. 이걸 하나라도 만족하면 그 칸은 검정.
	 * */
	
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringBuilder sb = new StringBuilder();
    
    static int s,N,K,R1,R2,C1,C2;

    public static void main(String[] args) throws IOException {
        init();
        process();
        print();

    }
    
    private static void init() throws IOException {
        
        StringTokenizer st = new StringTokenizer(br.readLine());
        s = Integer.parseInt(st.nextToken());
        N = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());
        R1 = Integer.parseInt(st.nextToken());
        R2 = Integer.parseInt(st.nextToken());
        C1 = Integer.parseInt(st.nextToken());
        C2 = Integer.parseInt(st.nextToken());

        

    }
    
  
    private static void process() {
    	for (int i = R1; i <= R2; i++) {
    		for (int j = C1; j <= C2; j++) {

    			boolean isBlack = check(i,j);
    			sb.append(isBlack?1:0);
    		}
    		sb.append("\n");
    	}

    }
    
    private static boolean check(int y,int x) {

    	for (int time = 1; time <= s; time++) {
    		int divisor = (int) Math.pow(N,time);
    		int yRemainder = y%divisor;
    		int xRemainder = x%divisor;
    		
    		int st = (N-K)/2 * (divisor/N);
    		int end = ((N+K)/2)* (divisor/N)-1;
    		
    		if(yRemainder >= st && yRemainder <= end 
    				&& xRemainder >= st && xRemainder <= end) return true;
    	}
    	return false;
    }
    

    private static void print() {
        System.out.print(sb);
    }
}
```
