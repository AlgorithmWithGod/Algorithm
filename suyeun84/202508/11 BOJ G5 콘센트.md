```java
import java.io.*;
import java.util.*;

public class boj23843 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}

	public static void main(String[] args) throws Exception {
		nextLine();
		int N = nextInt();
		int M = nextInt();
		int answer = 0;
		Integer[] t = new Integer[N];
		PriorityQueue<Integer> pq = new PriorityQueue<>();
		nextLine();
		for (int i = 0; i < N; i++) t[i] = nextInt();
		Arrays.sort(t);
		for (int i = 0; i < M; i++) {
            pq.add(0);
        }
        for (int i = N - 1; i >= 0; i--) {
            int tmp = pq.poll() + t[i];
            pq.add(tmp);
        }
        while (!pq.isEmpty()) {
        	answer = Math.max(pq.poll(), answer);
        }
        System.out.println(answer);
	}
}
```
