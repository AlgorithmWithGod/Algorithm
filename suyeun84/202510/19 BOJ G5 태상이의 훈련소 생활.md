```java
import java.io.*;
import java.util.*;

public class boj19951 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	static StringBuilder sb = new StringBuilder();

	public static void main(String[] args) throws Exception {
		nextLine();
		int N = nextInt();
		int M = nextInt();
		int[] arr = new int[N+1];
		nextLine();
		for(int i=1; i<arr.length; i++) {
			arr[i] = nextInt();
		}
		
		int[] dp = new int[N+2];
		for(int t=0; t<M; t++) {
			nextLine();
			int start = nextInt();
			int end = nextInt();
			int k = nextInt();
			
			dp[start] = dp[start]+k;
			dp[end+1] = dp[end+1]-k;
		}
		
		StringBuilder sb = new StringBuilder();
		for(int i=1; i<arr.length; i++) {
			dp[i] = dp[i]+dp[i-1];
			sb.append((arr[i]+dp[i])+ " ");
		}
		System.out.println(sb.toString());
	}
}
```
