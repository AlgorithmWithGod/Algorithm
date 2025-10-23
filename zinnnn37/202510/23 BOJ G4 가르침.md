```java
import java.io.*;
import java.util.StringTokenizer;

public class BJ_1062_가르침 {

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static       StringTokenizer st;

	private static int N, K, ans;
	private static String[]  words;
	private static boolean[] alpha;

	public static void main(String[] args) throws IOException {
		init();
		sol(0, 0);
		print(ans);
	}

	private static void init() throws IOException {
		st = new StringTokenizer(br.readLine());
		N = Integer.parseInt(st.nextToken());
		K = Integer.parseInt(st.nextToken());
		ans = 0;

		words = new String[N];
		for (int i = 0; i < N; i++) {
			words[i] = br.readLine();

			words[i] = words[i].replace("anta", "");
			words[i] = words[i].replace("tica", "");
		}

		if (K < 5) {
			print(0);
			System.exit(0);
		} else if (K >= 26) {
			print(N);
			System.exit(0);
		}
		K -= 5;

		alpha = new boolean[26];
		alpha[0] = true;
		alpha['n' - 'a'] = true;
		alpha['t' - 'a'] = true;
		alpha['i' - 'a'] = true;
		alpha['c' - 'a'] = true;
	}

	private static void sol(int depth, int start) {
		if (depth == K) {
			countAlpha();
			return;
		}

		for (int i = start; i < 26; i++) {
			if (alpha[i]) continue;

			alpha[i] = true;
			sol(depth + 1, i);
			alpha[i] = false;
		}
	}

	private static void countAlpha() {
		int     cnt = 0;
		boolean flag;
		for (String word : words) {
			flag = true;
			for (int i = 0; i < word.length(); i++) {
				if (!alpha[word.charAt(i) - 'a']) {
					flag = false;
					break;
				}
			}
			cnt += flag ? 1 : 0;
		}
		ans = Math.max(ans, cnt);
	}

	private static void print(int i) throws IOException {
		bw.write(i + "");
		bw.flush();
		bw.close();
		br.close();
	}

}
```