```java
import java.io.*;
import java.util.*;

public class boj1106 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	
	public static void main(String[] args) throws Exception {
		nextLine();
		int C = nextInt();
		int N = nextInt();
		int[] dp = new int[C+100];
		int answer = Integer.MAX_VALUE;
		Arrays.fill(dp, Integer.MAX_VALUE);
		dp[0] = 0;
		for (int i = 0; i < N; i++) {
			nextLine();
			int cost = nextInt();
			int num = nextInt();
			for (int j = num; j < C+100; j++) {
				if (dp[j - num] != Integer.MAX_VALUE) {
					dp[j] = Math.min(dp[j], dp[j-num] + cost);
				}
			}
		}
		for (int i = C; i < C+100; i++) answer = Math.min(answer, dp[i]);
		System.out.println(answer);
	}
}
```
