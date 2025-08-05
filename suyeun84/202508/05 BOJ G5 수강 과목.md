```java
import java.io.*;
import java.util.*;

public class boj17845 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	static StringBuilder sb = new StringBuilder();

	public static void main(String[] args) throws Exception {
		nextLine();
		int N = nextInt();
		int K = nextInt();
		int[] prior = new int[K+1];
		int[] time = new int[K+1];
		int[][] bag = new int[K+1][N+1];
		
		for (int i = 1; i <= K; i++) {
			nextLine();
			prior[i] = nextInt();
			time[i] = nextInt();
		}
		
		for (int i = 1; i <= K; i++) {
			for (int j = 1; j <= N; j++) {
				if (time[i] <= j) bag[i][j] = Math.max(bag[i-1][j], bag[i-1][j-time[i]] + prior[i]);
				else bag[i][j] = bag[i-1][j];
			}
		}
		System.out.println(bag[K][N]);
	}
}
```
