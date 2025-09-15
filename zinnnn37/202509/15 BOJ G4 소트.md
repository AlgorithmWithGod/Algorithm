```java
import java.io.*;
import java.util.StringTokenizer;

public class BJ_1083_소트 {

	private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
	private static       StringTokenizer st;

	private static int N, S;
	private static int[] nums;

	public static void main(String[] args) throws IOException {
		init();
		sol();
	}

	private static void init() throws IOException {
		N = Integer.parseInt(br.readLine());

		nums = new int[N];
		st   = new StringTokenizer(br.readLine());
		for (int i = 0; i < N; i++) {
			nums[i] = Integer.parseInt(st.nextToken());
		}

		S = Integer.parseInt(br.readLine());
	}

	private static void sol() throws IOException {
		if (N == 1) {
			print();
			return;
		}

		int idx = 0;
		while (S > 0 && idx < N) {
			int maxIdx = idx;

			// find max
			for (int i = idx; i < N; i++) {
				if (i > idx + S) break;
				
				if (nums[i] > nums[maxIdx]) {
					maxIdx = i;
				}
			}
			for (int j = maxIdx; j > idx; j--) {
				swap(j, j - 1);
				S--;
			}
			idx++;
		}
		print();
	}

	private static void swap(int a, int b) {
		int tmp = nums[a];
		nums[a] = nums[b];
		nums[b] = tmp;
	}

	private static void print() throws IOException {
		for (int i = 0; i < N; i++) {
			bw.write(nums[i] + " ");
		}
		bw.flush();
		bw.close();
		br.close();
	}

}
```