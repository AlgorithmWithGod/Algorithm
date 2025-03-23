```java
import java.io.*;
import java.util.*;

public class boj2623 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	
	public static void main(String[] args) throws Exception {
		nextLine();
		int N = nextInt();
		int M = nextInt();
		int[] cnt = new int[N+1];
		ArrayList<Integer> answer = new ArrayList<>();
		ArrayList<ArrayList<Integer>> graph = new ArrayList<>();
		for (int i = 0; i < N+1; i++) graph.add(new ArrayList<>());
		
		for (int i = 0; i < M; i++) {
			nextLine();
			int num = nextInt();
			int prev = nextInt();
			for (int j = 0; j < num-1; j++) {
				int curr = nextInt();
				graph.get(prev).add(curr);
				cnt[curr]++;
				prev = curr;
			}
		}
		while (answer.size() != N) {
			boolean flag = true;
			for (int i = 1; i < N+1; i++) {
				if (cnt[i] == 0) {
					cnt[i] = -1;
					answer.add(i);
					for (int next : graph.get(i)) {
						cnt[next]--;
					}
					flag = false;
				}
			}
			if (flag) {
				System.out.println(0);
				return;
			}
		}
		for (int i = 0; i < N; i++) {
			System.out.println(answer.get(i));
		}
	}
}

```
