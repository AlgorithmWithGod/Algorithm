```java
import java.io.*;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception { st = new StringTokenizer(br.readLine()); }
    static int nextInt() { return Integer.parseInt(st.nextToken()); }
    
	public static void main(String[] args) throws Exception {
		nextLine();
		int answer = Integer.MIN_VALUE;
		int N = nextInt();
		int[] honey = new int[N+1];
		int[][] sum = new int[2][N+2];
		nextLine();
		for (int i = 1; i <= N; i++) honey[i] = nextInt();
		for (int i = 1; i <= N; i++) {
			sum[0][i] = sum[0][i-1] + honey[i]; // 왼오
			sum[1][N-i+1] = sum[1][N-i+2] + honey[N-i+1]; // 오왼
		}
		// 벌통 오른쪽 끝
		for(int i = 2; i <= N-1; i++){
		    int cur = (sum[0][N] - sum[0][1] - honey[i]) + (sum[0][N] - sum[0][i]);
		    answer = Math.max(answer, cur);
		}
		// 벌통 왼쪽 끝
		for(int i = N-1; i >= 2; i--){
		    int cur = (sum[1][1] - sum[1][N] - honey[i]) + (sum[1][1] - sum[1][i]);
		    answer = Math.max(answer, cur);
		}
		// 벌통 가운데
		for(int i = 2; i <= N-1; i++){
		    answer = Math.max(answer, (sum[0][i] - sum[0][1]) + (sum[1][i] - sum[1][N]));
		}
		System.out.println(answer);
	}
}
```
