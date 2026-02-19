```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main {
	static int N;
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		N = Integer.parseInt(br.readLine());
		//1자리 소수로 모두 시작
		startTo(1, 2, N);
		startTo(1, 3, N);
		startTo(1, 5, N);
		startTo(1, 7, N);
	}

	private static void startTo(int depth, int value, int n) {
		if (!isPrime(value)) {
			return;
		}
		if (depth == n) {
			System.out.println(value);
			return;
		}
		
		
		for (int digit = 1; digit <= 9; digit++) {
			int next = value * 10 + digit;
			startTo(depth + 1, next, n);
		}
	}

	private static boolean isPrime(int num) {
		if (num < 2) {
			return false;
		}
		for (int i = 2; i * i <= num; i++) {
			if (num % i == 0) {
				return false;
			}
		}
		return true;
	}
}

```
