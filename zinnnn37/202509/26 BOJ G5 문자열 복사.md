```java
import java.io.*;

public class BJ_2195_문자열_복사 {

	private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

	private static String needle, haystack;

	public static void main(String[] args) throws IOException {
		sol();
	}

	private static void sol() throws IOException {
		needle   = br.readLine();
		haystack = br.readLine();

		int cnt   = 0;
		int start = 0;
		int len   = haystack.length();
		while (start < len) {
			int end = start + 1;

			while (end <= len && needle.indexOf(haystack.substring(start, end)) != -1) {
				end++;
			}

			start = end - 1;
			cnt++;
		}

		bw.write(cnt + "\n");
		bw.flush();
		bw.close();
		br.close();
	}

}
```