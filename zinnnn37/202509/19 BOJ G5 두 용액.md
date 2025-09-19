```java
import java.io.*;
import java.util.Arrays;
import java.util.StringTokenizer;

public class BJ_2470_두_용액 {

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static       StringTokenizer st;

	private static int   N;
	private static int   tmp;
	private static int[] ans;
	private static int[] solution;

	public static void main(String[] args) throws IOException {
		init();
		sol();
	}

	private static void init() throws IOException {
		N   = Integer.parseInt(br.readLine());
		tmp = Integer.MAX_VALUE;

		ans      = new int[2];
		solution = new int[N];
		st       = new StringTokenizer(br.readLine());
		for (int i = 0; i < N; i++) {
			solution[i] = Integer.parseInt(st.nextToken());
		}
		Arrays.sort(solution);
	}

	private static void sol() throws IOException {
		int left = 0, right = N - 1;

		while (left < right) {
			int sum = solution[left] + solution[right];

			if (Math.abs(sum) <= tmp) {
				ans[0] = solution[left];
				ans[1] = solution[right];

				tmp = Math.abs(sum);

				if (sum == 0) {
					break;
				}
			}

			if (sum < 0) {
				left++;
			} else {
				right--;
			}
		}
		bw.write(ans[0] + " " + ans[1]);
		bw.flush();
		bw.close();
		br.close();
	}

}
```