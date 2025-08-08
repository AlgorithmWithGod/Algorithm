```java
import java.io.*;
import java.util.*;

public class boj12931 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}

	public static void main(String[] args) throws Exception {
		nextLine();
		int N = nextInt();
		nextLine();
		int add = 0, multi = 0;
		for (int i = 0; i < N; i++) {
			int b = nextInt();
			int cnt = 0;
			while (b > 0) {
				if (b % 2 == 1) {
					b--;
					add++;
				} else {
					b /= 2;
					cnt++;
				}
			}
			multi = Math.max(multi, cnt);
		}
		System.out.println(add + multi);
	}
}
```
