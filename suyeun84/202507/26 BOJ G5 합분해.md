```java
import java.io.*;
import java.util.*;

public class boj2225 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	
	public static void main(String[] args) throws Exception {
		nextLine();
		int N = nextInt();
		int K = nextInt();
		
		long [][]dp=new long [N+1][K+1];
		
		for(int i = 1; i <= N; i++) {
			for(int j = 1; j <= K; j++) {
				dp[i][j] = 1; 
				for(int k = 1; k <= N; k++) {
					dp[i][j] += dp[k][j-1] % 1000000000;
				}
			}
		}	
		System.out.println(dp[N][K] % 1000000000);
	}
}
```
