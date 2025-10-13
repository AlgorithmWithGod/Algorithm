```java
import java.io.*;
import java.util.Stack;

public class BJ_2504_괄호의_값 {

	private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

	private static int ans, tmp, len;
	private static String str;

	private static Stack<Character> stack;

	public static void main(String[] args) throws IOException {
		init();
		sol();
	}

	private static void init() throws IOException {
		str   = br.readLine();
		len   = str.length();
		ans   = 0;
		tmp   = 1;
		stack = new Stack<>();
	}

	private static void sol() throws IOException {
		for (int i = 0; i < len; i++) {
			char c = str.charAt(i);

			if (c == '(') {
				tmp *= 2;
				stack.push(c);
			} else if (c == '[') {
				tmp *= 3;
				stack.push(c);
			} else {
				if (stack.isEmpty() || c == ')' && stack.peek() != '(' || c == ']' && stack.peek() != '[') {
					ans = 0;
					break;
				}

				if (c == ')') {
					if (str.charAt(i - 1) == '(') {
						ans += tmp;
					}
					tmp /= 2;
					stack.pop();
				} else if (c == ']') {
					if (str.charAt(i - 1) == '[') {
						ans += tmp;
					}
					tmp /= 3;
					stack.pop();
				}
			}
		}

		if (!stack.isEmpty()) {
			ans = 0;
		}
		
		bw.write(ans + "");
		bw.flush();
		bw.close();
		br.close();
	}

}
```