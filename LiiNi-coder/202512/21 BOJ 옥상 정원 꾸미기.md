```java
import java.io.*;
import java.util.*;

public class Main {
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int N = Integer.parseInt(br.readLine());
		long answer = 0L;
		
		Deque<Integer> stack = new ArrayDeque<>();

		for(int i = 0; i < N; i++){
			int height = Integer.parseInt(br.readLine());
			while(!stack.isEmpty() && stack.peekLast() <= height){
				stack.pollLast();
			}

			answer += stack.size();
			stack.offerLast(height);
		}
		System.out.println(answer);
	}
}

```
