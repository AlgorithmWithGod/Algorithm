```java
import java.io.*;
import java.util.*;

public class boj7983 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	static StringBuilder sb = new StringBuilder();

	public static void main(String[] args) throws Exception {
		nextLine();
		int n = nextInt();
		Task[] task = new Task[n];
		for (int i = 0; i < n; i++) {
			nextLine();
			int d = nextInt();
			int t = nextInt();
			task[i] = new Task(d, t);
		}
		Arrays.sort(task, (o1, o2) -> {
			return o2.end - o1.end;
		});
		
		int answer = task[0].end;
		for(int i = 0; i < n; i++) {
			if(task[i].end <= answer) answer = task[i].end - task[i].time;	
			else answer -= task[i].time;
		}
		System.out.println(answer);
	}
	static class Task {
		int time, end;
		public Task(int time, int end) {
			this.time = time;
			this.end = end;
		}
	}
}
```
