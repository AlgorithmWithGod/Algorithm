```java
import java.io.*;
import java.util.*;

class boj9024 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
    static int nextInt() {return Integer.parseInt(st.nextToken());}
    
	public static void main(String[] args) throws Exception {
        nextLine();
		int t = nextInt();
		while (t-- > 0) {
			nextLine();
			int n = nextInt();
			int k = nextInt();

			int[] arr = new int[n];
			nextLine();
			for (int i = 0; i < n; i++) {
				arr[i] = nextInt();
			}

			Arrays.sort(arr);
			int left = 0;
			int right = arr.length - 1;
			int best = (int)(2 * 10e8);
			int count = 1;

			while (true) {
				int sum = arr[left] + arr[right];

				if (Math.abs(sum - k) == best) {
					count++;
				} else if (Math.abs(sum - k) < best) {
					count = 1;
					best = Math.abs(sum - k);
				}

				if (sum == k) {
					left++;
					right--;
				} else if (sum < k) left++;
                else right--;

				if (left >= right) {
					break;
				}
			}
			System.out.println(count);
		}
	}
}
```
