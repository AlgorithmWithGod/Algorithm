```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main {
	private static BufferedReader br;
	private static int n;
	private static StringBuilder answer;
	private static boolean found;

	public static void main(String[] args) throws IOException {
		br = new BufferedReader(new InputStreamReader(System.in));
		n = Integer.parseInt(br.readLine());
		answer = new StringBuilder();
		found = false;
		recur(0, new StringBuilder());
		System.out.println(answer);
	}

	private static void recur(int depth, StringBuilder sb) {
		if (found) return;

		if (depth == n) {
			answer.append(sb);
			found = true;
			return;
		}

		for (int i = 1; i <= 3; i++) {
			sb.append(i);
			if (isGood(sb)) {
				recur(depth + 1, sb);
			}
			sb.deleteCharAt(sb.length() - 1);
		}
	}

	private static boolean isGood(StringBuilder sb) {
		int len = sb.length();
		for (int size = 1; size <= len / 2; size++) {
			String left = sb.substring(len - size * 2, len - size);
			String right = sb.substring(len - size, len);
			if (left.equals(right)) {
				return false;
			}
		}
		return true;
	}
}
```
