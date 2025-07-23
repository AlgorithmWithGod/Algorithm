```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;
import java.util.Arrays;

public class Main {
	private static BufferedReader br;
	private static int[] charCount; // 각 문자 a~z의 개수
	private static char[] inputChars;
	private static char[] output;
	private static int length;
	private static StringBuilder sb;

	public static void main(String[] args) throws IOException {
		br = new BufferedReader(new InputStreamReader(System.in));
		int t = Integer.parseInt(br.readLine());
		sb = new StringBuilder();

		for (int testCase = 0; testCase < t; testCase++) {
			inputChars = br.readLine().toCharArray();
			Arrays.sort(inputChars);
			length = inputChars.length;
			output = new char[length];
			charCount = new int[26];

			for (char c : inputChars) {
				charCount[c - 'a']++;
			}

			permute(0);
		}
		System.out.print(sb);
	}

	private static void permute(int depth) {
		if (depth == length) {
			sb.append(output).append('\n');
			return;
		}

		for (int i = 0; i < 26; i++) {
			if (charCount[i] > 0) {
				output[depth] = (char) ('a' + i);
				charCount[i]--;
				permute(depth + 1);
				charCount[i]++;
			}
		}
	}
}
```
