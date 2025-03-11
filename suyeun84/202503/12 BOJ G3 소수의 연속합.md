```java
import java.io.*;
import java.util.*;

public class boj1644 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    
	static int N;
	static boolean[] isPrime;
	static boolean flag = false;
	public static void main(String[] args) throws Exception {
		N = Integer.parseInt(br.readLine());
		int start = 2, end = 3, res = 5, answer = 0;
		isPrime = new boolean[N+1];
		primeCheck();
		if (N == 5) answer = 1;
		if (isPrime[N]) answer++;
		while (start < end) {
			if (res < N) {
				end = nextIdx(end);
				res += end;
			} else if (res >= N) {
				res -= start;
				start = nextIdx(start);
			}
			if (res == N && start != end) {
				answer++;
			}
			if (flag) break;
		}
		System.out.println(answer);

	}
	static void primeCheck() {
		Arrays.fill(isPrime, true);
		isPrime[0] = false;
		isPrime[1] = false;
		for (int i = 2; i <= Math.sqrt(N+1); i++) {
			if(isPrime[i]) {
				for (int j = i*i; j <= N; j+=i) {
					isPrime[j] = false;
				}
			}
		}
	}
	
	static int nextIdx(int idx) {
		for (int i = idx+1; i <= N; i++) {
			if (isPrime[i]) return i;
		}
		flag = true;
		return idx;
	}
}
```
