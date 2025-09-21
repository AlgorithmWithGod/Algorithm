```java
import java.io.*;

public class BJ_6443_애너그램 {

	private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

	private static String input;
	private static int    length;
	private static int[]  alphabets;
	private static char[] result;

	public static void main(String[] args) throws IOException {
		int T = Integer.parseInt(br.readLine());

		while (T-- > 0) {
			sol();
		}
		bw.flush();
		bw.close();
		br.close();
	}

	private static void sol() throws IOException {
		input     = br.readLine();
		length    = input.length();
		alphabets = new int[26];
		result    = new char[length];

		for (int i = 0; i < length; i++) {
			alphabets[input.charAt(i) - 'a']++;
		}
		perm(0);
	}

	private static void perm(int depth) throws IOException {
		if (depth == length) {
			bw.write(result);
			bw.write('\n');
			return;
		}

		for (int i = 0; i < 26; i++) {
			if (alphabets[i] > 0) {
				alphabets[i]--;
				result[depth] = (char) (i + 'a');
				perm(depth + 1);
				alphabets[i]++;
			}
		}
	}
}
```