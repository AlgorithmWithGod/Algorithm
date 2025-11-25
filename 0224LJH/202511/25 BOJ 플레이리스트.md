```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

public class Main {
	
	// dp[i][j]: i번째까지 k개의 숫자로 채운 경우
	// -> dp[i]
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static long[][] dp;
	static int songCnt, minDis, totalLen;
	
	static final long DIVISOR = 1_000_000_007l;
	
    public static void main(String[] args) throws IOException {

        init();
        process();
    	print();

    }
    
    private static void init() throws IOException{
    	StringTokenizer st = new StringTokenizer(br.readLine());
    	songCnt = Integer.parseInt(st.nextToken());
    	minDis = Integer.parseInt(st.nextToken());
    	totalLen = Integer.parseInt(st.nextToken());
    	dp = new long[totalLen+1][songCnt+1];
    	dp[1][1] = songCnt;
    }
    
    private static void process() throws IOException {
    	for (int i = 2; i <= totalLen; i++) {
    		if (i <= minDis) {
    			// 아직 총 길이가 간격보다 적은 경우. 
    			// 그냥 i개의 노래로 줄세우는 것과 동일하다.
    			dp[i][i] = (dp[i-1][i-1] * (songCnt-i+1))%DIVISOR;
    			continue;
    		}
    		
    		//적어도 minDis개 만큼의 부분배열에서는 겹치는게 없다는 것을 고려하자
    		for (int j = 1; j <= songCnt; j++) {
    			if (dp[i-1][j] == 0) continue;
    			
    			//이전에 있는 것과 동일한 것을 선택하는 경우
    			//이 경우, curSongCnt - minDis개의 선택지가 존재하게 된다.
    			dp[i][j] += dp[i-1][j] * (j - minDis);
    			dp[i][j] %= DIVISOR;
    			
    			// 이전과 다른 것을 선택하는 경우
    			if (j == songCnt) continue;
    			dp[i][j+1] += dp[i-1][j] * (songCnt - j);
    			dp[i][j+1] %= DIVISOR;
    		}
    	}
    	
    }
    

    
    

    
    

	private static void print() {
		System.out.println(dp[totalLen][songCnt]);
    }

}
```
