```java
import java.io.*;
import java.util.*;

public class boj11265 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	static StringBuilder sb = new StringBuilder();
	
	public static void main(String[] args) throws Exception {
		nextLine();
		int N = nextInt();
		int M = nextInt();
		int[][] cost = new int[N+1][N+1];
		for (int i = 1; i < N+1; i++) {
			nextLine();
			for(int j = 1; j < N+1; j++){
                cost[i][j] = nextInt();
            }
		}
		for(int middle = 1; middle < N+1; middle++){
            for(int start = 1; start < N+1; start++){
                for(int end = 1; end < N+1; end++){
                    cost[start][end] = Math.min(cost[start][end], cost[start][middle]+cost[middle][end]);
                }
            }
        }
		for (int i = 0; i < M; i++) {
			nextLine();
			int a = nextInt();
			int b = nextInt();
			long c = Long.parseLong(st.nextToken());
			if(cost[a][b] <= c) {
                sb.append("Enjoy other party").append("\n");
            } else {
              sb.append("Stay here").append("\n");
            }
        }
        System.out.println(sb);
	}
}
```
