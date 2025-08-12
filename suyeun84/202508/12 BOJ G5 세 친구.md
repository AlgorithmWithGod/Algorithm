```java
import java.io.*;
import java.util.*;

public class boj17089 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}

	public static void main(String[] args) throws Exception {
		nextLine();
		int N = nextInt();
		int M = nextInt();
		boolean[][] friend = new boolean[N+1][N+1];
        int[] count = new int[N+1];
		for (int i = 0; i < M; i++) {
			nextLine();
			int a = nextInt();
			int b = nextInt();
			friend[a][b] = true;
			friend[b][a] = true;
			count[a]++;
			count[b]++;
		}
		
		int min = Integer.MAX_VALUE;

        for(int A = 1; A < N+1; A++) {
            for(int B = A+1; B < N+1; B++) {
                if(!friend[A][B]) continue;
                for(int C = B+1; C < N+1; C++) {
                    if(!friend[C][A] || !friend[C][B]) continue;

                    int sum = count[A] + count[B] + count[C] - 6;
                    min = Math.min(min, sum);
                }
            }
        }

        if(min == Integer.MAX_VALUE) System.out.println(-1);
        else System.out.println(min);
	}
}
```
