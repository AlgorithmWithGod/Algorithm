```java
import java.util.*;
import java.io.*;

class IOController {
	BufferedReader br;
	BufferedWriter bw;
	StringTokenizer st;

	public IOController() {
		br = new BufferedReader(new InputStreamReader(System.in));
		bw = new BufferedWriter(new OutputStreamWriter(System.out));
		st = new StringTokenizer("");
	}

	String nextLine() throws Exception {
		String line = br.readLine();
		st = new StringTokenizer(line);
		return line;
	}

	String nextToken() throws Exception {
		while (!st.hasMoreTokens()) nextLine();
		return st.nextToken();
	}

	int nextInt() throws Exception {
		return Integer.parseInt(nextToken());
	}

	long nextLong() throws Exception {
		return Long.parseLong(nextToken());
	}

	double nextDouble() throws Exception {
		return Double.parseDouble(nextToken());
	}

	void close() throws Exception {
		bw.flush();
		bw.close();
	}

	void write(String content) throws Exception {
		bw.write(content);
	}

}

public class Main {

	static IOController io;

	//

	static int N;
	static List<int[]>[] graph;
	static List<Integer> list;

	public static void main(String[] args) throws Exception {

		io = new IOController();

		N = io.nextInt();
		list = new ArrayList<>();
		graph = new List[N+1];
		for(int i=1;i<=N;i++) graph[i] = new ArrayList<>();
		for(int i=1;i<N;i++) {
			int a = io.nextInt();
			int b = io.nextInt();
			int c = io.nextInt();
			graph[a].add(new int[]{b,c});
			graph[b].add(new int[]{a,c});
		}

		Queue<int[]> q = new ArrayDeque<>();
		boolean[] vis = new boolean[N+1];
		q.offer(new int[]{1,0});
		vis[1] = true;
		while(!q.isEmpty()) {
			int[] cur = q.poll();
			int n = cur[0], v = cur[1];
			list.add(v);
			for(int[] e:graph[n]) if(!vis[e[0]]) {
				vis[e[0]] = true;
				q.offer(new int[]{e[0],v^e[1]});
			}
		}
		Collections.sort(list);

		long ans = 0, cnt = 1;
		int prev = list.get(0);
		for(int i=1;i<N;i++) {
			int v = list.get(i);
			if(v != prev) {
				ans += cnt*(cnt-1)/2;
				cnt = 0;
			}
			cnt++;
			prev = v;
		}
		ans += cnt*(cnt-1)/2;

		io.write(ans + "\n");

		io.close();

	}

}
```
