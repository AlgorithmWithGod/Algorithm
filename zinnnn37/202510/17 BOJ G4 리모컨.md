```java
import java.io.*;
import java.util.StringTokenizer;

public class BJ_1107_리모컨 {

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static       StringTokenizer st;

	private static int N, M, ans;
	private static String[] malfunctioningButtons;

	public static void main(String[] args) throws IOException {
		init();
		sol();
	}

	private static void init() throws IOException {
		N = Integer.parseInt(br.readLine());
		M = Integer.parseInt(br.readLine());
		ans = Math.abs(N - 100);

		malfunctioningButtons = new String[M];

		if (M > 0) {
			st = new StringTokenizer(br.readLine());
			for (int i = 0; i < M; i++) {
				malfunctioningButtons[i] = st.nextToken();
			}
		}
	}

	private static void sol() throws IOException {
		for (int i = 0; i <= 1000000; i++) {
			String check = String.valueOf(i);

			boolean flag = true;
			for (String malfunctioningButton : malfunctioningButtons) {
				if (check.contains(malfunctioningButton)) {
					flag = false;
					break;
				}
			}
			if (flag) {
				ans = Math.min(ans, check.length() + Math.abs(N - i));
			}
		}

		bw.write(ans + "");
		bw.flush();
		bw.close();
		br.close();
	}

}
```