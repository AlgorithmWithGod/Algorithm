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
	static int[] a;

	public static void main(String[] args) throws Exception {

		io = new IOController();

		N = io.nextInt();
		a = new int[N];
		int min = Integer.MAX_VALUE;
		for(int i=0;i<N;i++) {
			a[i] = io.nextInt();
			min = Math.min(min, a[i]);
		}

		for(int i=0;i<N;i++) a[i] -= min;

		Arrays.sort(a);
		if(a[1] == 0) {
			io.write("No");
			io.close();
			return;
		}
		int last = a[1], d = a[1], c = 2;
		boolean[] vis = new boolean[N];
		for(int i=2;i<N;i++) {
			if(a[i] == d*c) {
				last = d*c;
				c++;
				vis[i] = true;
			}
		}

		List<Integer> list = new ArrayList<>();
		for(int i=2;i<N;i++) if(!vis[i]) list.add(a[i]);

		d = list.get(0);
		c = 2;
		boolean can = true;
		for(int i=1;i<list.size();i++) {
			int cur = list.get(i);
			if(cur == d*c) c++;
			else can = false;
		}

		if(!can) {
			list.add(last);
			Collections.sort(list);
			d = list.get(0);
			c = 2;
			can = true;
			for(int i=1;i<list.size();i++) {
				int cur = list.get(i);
				if(cur == d*c) c++;
				else can = false;
			}
		}

		io.write(can ? "Yes" : "No");

		io.close();

	}

}
```
