```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main {
	static long[] Prefix;
	static long Total;

	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int N = Integer.parseInt(br.readLine().trim());
		long[] dist = new long[N];
		for(int i = 0; i < N; i++) {
			dist[i] = Long.parseLong(br.readLine());
		}

		//원형 -> 배열을 2배
		Prefix = new long[2*N + 1];
		for(int i = 0; i < 2 * N; i++) {
			Prefix[i + 1] = Prefix[i] + dist[i % N];
		}
		Total = Prefix[N];
		long answer = 0;
		for(int i = 0; i < N; i++) {
			int l = i;
			int r = i + N;
			while(l + 1 < r) {
				int mid = (l+r) / 2;
				if(check(i, mid) == check(i, l)) {
					l = mid;
				}else {
					r = mid;
				}
			}
			long clockwise = Prefix[l] - Prefix[i];
			answer = Math.max(answer, clockwise);
		}

		System.out.println(answer);
	}

	static boolean check(int i, int mid) {
		return (Prefix[mid] - Prefix[i]<= Total/2);
	}
}

```
