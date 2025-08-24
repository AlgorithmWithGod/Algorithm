```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;


public class Main {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static int coinCnt,goal,ans;
	static int[] coin,dp;
	


	public static void main(String[] args) throws IOException {
		int TC = Integer.parseInt(br.readLine());
		for (int tc = 1; tc <= TC; tc++) {
			init();
			process();
			print();
		}
	}
   
	public static void init() throws IOException {
		coinCnt = Integer.parseInt(br.readLine());
		coin = new int[coinCnt];
		ans = 0;
		
		StringTokenizer st = new StringTokenizer(br.readLine());
		for (int i = 0; i < coinCnt; i++) {
			coin[i] = Integer.parseInt(st.nextToken());
		}
		goal = Integer.parseInt(br.readLine());
		dp = new int[goal+1];
		dp[0] = 1;

	}
   
	public static void process() {
		for (int i = 0; i < coinCnt; i++) {
			int num = coin[i];
			for (int j = 0; j <= goal - num; j++) {
				dp[j+num] += dp[j];
			}
		}
		ans = dp[goal];
		
	}

         

   
	public static void print() {
		System.out.println(ans);
	}
}
```
