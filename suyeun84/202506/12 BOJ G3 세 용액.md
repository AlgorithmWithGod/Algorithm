```java
import java.io.*;
import java.util.*;

public class boj2473 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	
	public static void main(String[] args) throws Exception {
		nextLine();
		int N = Integer.parseInt(st.nextToken());
		long[] num = new long[N];
		long answer = Long.MAX_VALUE;
		long[] res = new long[3]; 
		nextLine();
		for(int i = 0; i < N; i++) {
			num[i] = Long.parseLong(st.nextToken());
		}
		Arrays.sort(num);
		
		for (int i = 0; i < N; i++) {
			int start = i+1;
			int end = N-1;
			while (start < end) {
				long temp = num[i] + num[start] + num[end];
				if (Math.abs(temp) < answer) {
					res[0] = num[i];
					res[1] = num[start];
					res[2] = num[end];
					answer = Math.abs(temp);
				}
				if (temp > 0) end--;
				else if (temp < 0) start++;
				else {
					System.out.println(res[0]+" "+res[1]+" "+res[2]);
					return;
				}
			}
		}
		System.out.println(res[0]+" "+res[1]+" "+res[2]);
	}
}                     
```
