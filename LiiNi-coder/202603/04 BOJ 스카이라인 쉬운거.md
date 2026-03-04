```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayDeque;
import java.util.StringTokenizer;

public class Main{
	public static void main(String[] args)throws IOException{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int N = Integer.parseInt(br.readLine());
		ArrayDeque<Integer> stack = new ArrayDeque<Integer>();

		int answer = 0;
		for(int i=0;i<N;i++){
			StringTokenizer st = new StringTokenizer(br.readLine());
			int x = Integer.parseInt(st.nextToken());
			int h = Integer.parseInt(st.nextToken());

			while(!stack.isEmpty()){
				if(stack.peek() <= h) break;
				stack.pop();
				answer++;
			}


			if(h==0) continue;

			if(stack.isEmpty() || stack.peek()<h){
				stack.push(h);
			}
		}

		answer += stack.size();
		System.out.println(answer);
		br.close();
	}
}
```
