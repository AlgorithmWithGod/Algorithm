```java
import java.io.*;
import java.util.*;

public class boj22251 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
    static int nextInt() {return Integer.parseInt(st.nextToken());}
    
    static int[][] digit = {
            {0, 4, 3, 3, 4, 3, 2, 3, 1, 2},
            {4, 0, 5, 3, 2, 5, 6, 1, 5, 4},
            {3, 5, 0, 2, 5, 4, 3, 4, 2, 3},
            {3, 3, 2, 0, 3, 2, 3, 2, 2, 1},
            {4, 2, 5, 3, 0, 3, 4, 3, 3, 2},
            {3, 5, 4, 2, 3, 0, 1, 4, 2, 1},
            {2, 6, 3, 3, 4, 1, 0, 5, 1, 2},
            {3, 1, 4, 2, 3, 4, 5, 0, 4, 3},
            {1, 5, 2, 2, 3, 2, 1, 4, 0, 1},
            {2, 4, 3, 1, 2, 1, 2, 3, 1, 0}
    };
    static int N, K, P, X, answer;
	public static void main(String[] args) throws Exception {
		nextLine();
		N = nextInt(); // N층까지 이용 가능
		K = nextInt(); // 숫자 길이
		P = nextInt(); // 1~P개 반전
		X = nextInt(); // 실제 층
		
		solve(0, 1, 0, 0);
			
		System.out.println(answer-1);
	}
	
	static void solve(int idx, int ten, int now, int cnt) {
		if (now > N || cnt > P) return;
		if (idx == K) {
			if (now != 0) answer++;
			return;
		}
		for(int i = 0; i < 10; i++) {
			solve(idx+1, ten*10, i*ten+now, cnt+digit[X/ten%10][i]);
		}
	}
}

```
