```java
import java.io.*;
import java.util.Arrays;
import java.util.StringTokenizer;

public class BJ_2096_내려가기 {

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static       StringTokenizer st;

	private static int N, minAns, maxAns;
	private static int[][] nums, min, max;

	public static void main(String[] args) throws IOException {
		init();
		sol();
	}

	private static void init() throws IOException {
		N = Integer.parseInt(br.readLine());

		minAns = Integer.MAX_VALUE;
		maxAns = 0;

		nums = new int[N][3];
		min  = new int[N][3];
		max  = new int[N][3];

		for (int i = 0; i < N; i++) {
			st = new StringTokenizer(br.readLine());
			for (int j = 0; j < 3; j++) {
				nums[i][j] = Integer.parseInt(st.nextToken());
			}
		}

		for (int i = 0; i < N; i++) {
			Arrays.fill(min[i], Integer.MAX_VALUE);
		}

		for (int i = 0; i < 3; i++) {
			min[0][i] = nums[0][i];
			max[0][i] = nums[0][i];
		}

	}

	private static void sol() throws IOException {
		for (int i = 1; i < N; i++) {
			for (int j = 0; j < 3; j++) {
				for (int k = j - 1; k <= j + 1; k++) {
					if (k < 0 || k == 3) continue;

					min[i][j] = Math.min(min[i][j], nums[i][j] + min[i - 1][k]);
					max[i][j] = Math.max(max[i][j], nums[i][j] + max[i - 1][k]);
				}
			}
		}

		for (int i = 0; i < 3; i++) {
			minAns = Math.min(minAns, min[N - 1][i]);
			maxAns = Math.max(maxAns, max[N - 1][i]);
		}

		bw.write(maxAns + " " + minAns);
		bw.flush();
		bw.close();
		br.close();
	}

}
```