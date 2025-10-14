```java
import java.io.*;
import java.util.*;

public class boj2073 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception { st = new StringTokenizer(br.readLine()); }
    static int nextInt() { return Integer.parseInt(st.nextToken()); }
    
	public static void main(String[] args) throws Exception {
		nextLine();
		int D = nextInt();
		int P = nextInt();
		int[] dp = new int[D+1];
		dp[0] = Integer.MAX_VALUE;
		for (int i = 0; i < P; i++) {
			nextLine();
			int L = nextInt(); //길이
			int C = nextInt(); //용량
			for (int j = D; j >= L; j--) {
				dp[j] = Math.max(dp[j], Math.min(C, dp[j-L]));
			}
		}
		System.out.println(dp[D]);
	}
}
```
