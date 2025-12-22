```java
import java.io.*;
import java.util.*;

public class Main {
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(
			new InputStreamReader(System.in)
		);
		int N = Integer.parseInt(br.readLine());
		StringTokenizer st = new StringTokenizer(br.readLine());
		int[] arr = new int[N];
		for(int i = 0; i < N; i++){
			arr[i] = Integer.parseInt(st.nextToken());
		}
		int[] answer = new int[N];
		Arrays.fill(answer, -1);
		Deque<Integer> stack = new ArrayDeque<>();

		for(int i = 0; i < N; i++){
			while(!stack.isEmpty() && arr[stack.peekLast()] < arr[i]){
				int index = stack.pollLast();
				answer[index] = arr[i];
			}
			stack.offerLast(i);
		}
		StringBuilder sb = new StringBuilder();
		for(int v : answer){
			sb.append(v).append(" ");
		}

		System.out.println(sb.toString());
	}
}

```
