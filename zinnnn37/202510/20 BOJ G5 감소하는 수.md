```java
import java.io.*;
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class BJ_1038_감소하는_수 {

	private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

	private static int        N;
	private static List<Long> nums;

	public static void main(String[] args) throws IOException {
		if (init()) {
			for (int i = 0; i <= 9; i++) {
				sol(i);
			}
			Collections.sort(nums);
			bw.write(nums.get(N) + "");
		}
		bw.flush();
		bw.close();
		br.close();
	}

	private static boolean init() throws IOException {
		N = Integer.parseInt(br.readLine());

		if (N <= 10) {
			bw.write(N + "");
			return false;
		} else if (N >= 1023) {
			bw.write("-1");
			return false;
		}
		nums = new ArrayList<>();

		return true;
	}

	private static void sol(long num) throws IOException {
		nums.add(num);

		long mod = num % 10;
		if (mod == 0) return;

		for (int i = 0; i < mod; i++) {
			sol(num * 10 + i);
		}
	}

}
```