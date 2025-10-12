```java
import java.io.*;
import java.util.Arrays;
import java.util.StringTokenizer;

public class BJ_1759_암호_만들기 {

	private static final String VOWELS = "aeiou";

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static final StringBuilder   sb = new StringBuilder();
	private static       StringTokenizer st;

	private static int L, C;
	private static String[] chars;
	private static int[]    candidate;

	public static void main(String[] args) throws IOException {
		init();
		sol(0, 0, 0, 0);

		bw.write(sb.toString());
		bw.flush();
		bw.close();
		br.close();
	}

	private static void init() throws IOException {
		st = new StringTokenizer(br.readLine());
		L  = Integer.parseInt(st.nextToken());
		C  = Integer.parseInt(st.nextToken());

		chars     = new String[C];
		candidate = new int[L];
		st        = new StringTokenizer(br.readLine());
		for (int i = 0; i < C; i++) {
			chars[i] = st.nextToken();
		}
		Arrays.sort(chars);
	}

	private static void sol(int depth, int start, int vowels, int consonants) {
		if (depth == L) {
			if (vowels >= 1 && consonants >= 2) {
				appendAns();
			}
			return;
		}

		for (int i = start; i < C; i++) {
			candidate[depth] = i;

			boolean isVowel = VOWELS.contains(chars[i]);

			sol(depth + 1, i + 1, isVowel ? vowels + 1 : vowels, isVowel ? consonants : consonants + 1);
		}
	}

	private static void appendAns() {
		for (int c : candidate) {
			sb.append(chars[c]);
		}
		sb.append("\n");
	}

}
```