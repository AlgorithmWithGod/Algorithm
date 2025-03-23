```java
import java.util.*;
import java.io.*;

public class Main {
	public static void main(String[] args) throws Exception {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		
		int N = Integer.parseInt(st.nextToken());
		int[][] work = new int[N][2];
		for (int i = 0; i < N; i++) {
			st = new StringTokenizer(br.readLine());
			int T = Integer.parseInt(st.nextToken());
			int S = Integer.parseInt(st.nextToken());
			
			work[i][0] = S;
			work[i][1] = T;
		}
		Arrays.sort(work, Comparator.comparingInt(a -> a[0]));

		int answer = work[0][0] - work[0][1];
		
		while (answer >= 0) {
			int curr = answer;
			boolean flag = true;
			for (int i = 0; i < N; i++) {
				if (curr + work[i][1] <= work[i][0]) {
					curr += work[i][1];
				} else {
					answer -= 1;
					flag = false;
					break;
				}
			}
			if (flag) {
				System.out.println(answer);
				return;
			}
		}
		System.out.println(-1);
	}
}
```
