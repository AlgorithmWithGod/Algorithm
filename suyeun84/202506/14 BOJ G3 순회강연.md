```java
import java.io.*;
import java.util.*;

public class boj2109 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	
	public static void main(String[] args) throws Exception {
		nextLine();
		int N = nextInt();
		int[][] arr = new int[N][2];
		int[] store = new int[10001];
		int answer = 0;
		for (int i = 0; i < N; i++) {
			nextLine();
			arr[i][0] = nextInt();
			arr[i][1] = nextInt();
		}
		Arrays.sort(arr, (o1, o2) -> {
			return o2[0] - o1[0];
		});
		for (int i = 0; i < N; i++) {
			int cost = arr[i][0];
			int day = arr[i][1];
			for (int j = day; j >= 1; j--) {
				if (store[j] < cost) {
					store[j] = cost;
					break;
				}
			}
		}
		for (int i = 0; i < 10001; i++) answer += store[i];
		System.out.println(answer);
	}
}
```
