```java
import java.io.*;

public class boj16472 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

	public static void main(String[] args) throws Exception {
		int N = Integer.parseInt(br.readLine());
		String input = br.readLine();
		int[] alpha = new int[26];
		int cnt = 0, answer = 0, start = 0, end = -1;
		
		while (++end < input.length()) {
            if (alpha[input.charAt(end) - 'a']++ == 0) cnt++;

            while (N < cnt) {
                if (--alpha[input.charAt(start++) - 'a'] == 0) cnt--;
            }

            answer = Math.max(answer, end - start + 1);
        }
        System.out.println(answer);
	}
}
```
