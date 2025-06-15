```java
import java.io.*;
import java.util.*;

public class boj2457 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	
	public static void main(String[] args) throws Exception {
		nextLine();
		int N = nextInt();
		Flower[] flowers = new Flower[N];
		for (int i = 0; i < N; i++) {
			nextLine();
			flowers[i] = new Flower(nextInt()*100 + nextInt(), nextInt()*100 + nextInt());	
		}
		Arrays.sort(flowers, (o1, o2)-> {
			if (o1.start == o2.start) return o2.end - o1.end;
			return o1.start - o2.start;
		});
		int start = 301;
		int end = 1201;
		int maxEnd = 0;
		int answer = 0;
		int idx = 0;
		while (start < end) {
			boolean flag = false;
			for (int i = idx; i < N; i++) {
				if (flowers[i].start > start) break;
				if (flowers[i].end > maxEnd) {
					maxEnd = flowers[i].end;
					idx = i+1;
					flag = true;
				}
			}
			if (flag) {
				answer++;
				start = maxEnd;
			} else break;
		}
		System.out.println(maxEnd < end ? "0" : answer);
	}
	
	static class Flower {
		int start, end;
		public Flower (int start, int end) {
			this.start = start;
			this.end = end;
		}
	}
}
```
