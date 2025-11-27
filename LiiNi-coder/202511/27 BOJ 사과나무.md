```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main{
	private static int N;
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		// 타겟 : x, y
		// x1, 가 등장하면, x1까지의 stack에 모두 표식
		// y1, y2가 등장한다면 이제 stack에서 pop될때 표식 되있는것이라면 그것 출력

		N = Integer.parseInt(br.readLine());

		String arr = br.readLine();
		char[] cs = arr.toCharArray();
		String temp1 = br.readLine();
		String[] temp = temp1.split(" ");
		int x = Integer.parseInt(temp[0]) - 1;
		int y = Integer.parseInt(temp[1]) - 1;
		Deque<int[]> stack = new ArrayDeque<>();

		int[][] indexesAtname = new int[N][2];

		int name = 0;
		boolean isFindMode = false;
		int[] popElement = null;

		for(int i = 0; i < arr.length(); i++) {
			char c = cs[i];
			if(c == '0'){
				// 넣기
				indexesAtname[name][0] = i;
				stack.push(new int[]{name++, 0});
			}else{
				// 빼기
				popElement = stack.pop();
				indexesAtname[popElement[0]][1] = i;
			}
		}
		name = 0;
		for(int i = 0; i < arr.length(); i++){
			char c = cs[i];
			if(i == x){
				for(int[] element: stack){
					element[1] = 1;
				}
			}else if(i == y){
				isFindMode = true;
			}
			if(c == '0'){
				// 넣기
				indexesAtname[name][0] = i;
				stack.push(new int[]{name++, 0});
				if(i == x){
					stack.peek()[1] = 1;
				}
			}else{
				// 빼기
				popElement = stack.pop();
				indexesAtname[popElement[0]][1] = i;
				if(isFindMode && popElement[1] == 1)
					break;
			}
		}

		StringBuilder sb = new StringBuilder();
		sb.append(indexesAtname[popElement[0]][0] + 1);
		sb.append(" ");
		sb.append(indexesAtname[popElement[0]][1] + 1);
		System.out.println(sb.toString());
		br.close();
	}
}
```
