```java
package boj;

import java.io.*;
import java.util.*;

public class boj2283 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception { st = new StringTokenizer(br.readLine()); }
    static int nextInt() { return Integer.parseInt(st.nextToken()); }
    
	public static void main(String[] args) throws Exception {
		nextLine();
		int N = nextInt();
		int K = nextInt();
		int start= 1000001;
		int end = 0;
		int[] num = new int[1000001];
		// 누적합 생성
		for (int i = 0; i < N; i++) {
			nextLine();
			int a = nextInt();
			int b = nextInt();
			num[a]++;
			num[b]--;
			start = Math.min(start, a);
			end = Math.max(end, b);
		}
		for (int i = start+1; i <= end; i++) {
			num[i] += num[i-1];
		}
		
		// 투 포인터
		int sum = 0;
		int s = 0;
		int e = start;
		while (e <= end) {
			if (sum < K) {
				sum += num[e];
				e++;
			} else if (sum == K) {
				System.out.println(s+" "+e);
				return;
			} else {
				sum -= num[s];
				s++;
			}
		}
		System.out.println(0+" "+0);
	}
}
```
