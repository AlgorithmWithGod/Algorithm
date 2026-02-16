```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main {
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		String s = br.readLine();
		int n = s.length();
		int MOD = 1_000_000;
		int[] dp = new int[n + 1];
		if (s.charAt(0) == '0') {
			System.out.println(0);
			return;
		}

		
		dp[0] = 1;
		dp[1] = 1;
		for (int i = 2; i <= n; i++) {
			char now = s.charAt(i - 1);
			char previous = s.charAt(i - 2);
			//한자리수
			if (now != '0') {
				dp[i] = (dp[i] + dp[i - 1]) % MOD;
			}

			//두자리수
			int twoDigit = (previous - '0') * 10 + (now - '0');
			if (twoDigit >= 10 && twoDigit <= 26) {
				dp[i] = (dp[i] + dp[i - 2]) % MOD;
			}
		}
		System.out.println(dp[n]);
	}
}

```
