```java
import java.util.*;
import java.io.*;

class Solution
{
	static Work[] works;
	
	public static void main(String[] args) throws Exception{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		
		int N = Integer.parseInt(st.nextToken());
		works = new Work[N];
		for (int i = 0; i < N; i++) {
			st = new StringTokenizer(br.readLine());
			works[i] = new Work(Integer.parseInt(st.nextToken()), Integer.parseInt(st.nextToken()));
		}
		
		Arrays.sort(works, (o1, o2) -> {
			if (o1.s != o2.s) return o1.s-o2.s;
			return o2.t-o1.t;
		});
		
		int answer = works[0].s - works[0].t;
		while (answer >= 0) {
			if (check(answer)) {
				System.out.println(answer);
				return;
			}
			answer -= 1;
		}
		System.out.println(-1);
	}
	
	static boolean check(int start) {
		int curr = start;
		for (Work w : works) {
			if (curr + w.t > w.s) return false;
			curr += w.t;
		}
		return true;
	}
	
	static class Work {
		int t;
		int s;
		public Work(int t, int s) {
			this.t = t;
			this.s = s;
		}
	}
}

```
