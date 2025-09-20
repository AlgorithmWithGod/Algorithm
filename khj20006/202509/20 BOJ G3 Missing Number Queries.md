```java
import java.io.*;
import java.util.*;

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
		while (!st.hasMoreTokens())
			nextLine();
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

	static int N, Q;
	static int[] cnt, a;
	static TreeSet<Integer> set;

	public static void main(String[] args) throws Exception {

		io = new IOController();

		N = io.nextInt();
		Q = io.nextInt();
		a = new int[N+1];
		cnt = new int[N+1];
		for(int i=1;i<=N;i++) {
		    a[i] = io.nextInt();
		    cnt[a[i]]++;
		}
		
		set = new TreeSet<>();
		for(int i=1;i<=N;i++) if(cnt[i] == 0) set.add(i);
		
		for(int i=0;i<Q;i++) {
		    int op = io.nextInt();
		    int x = io.nextInt();
		    int y = io.nextInt();
		    if(op == 1) {
		        int prev = a[x];
		        if(--cnt[prev] == 0) set.add(prev);
		        if(cnt[y]++ == 0) set.remove(y);
		        a[x] = y;
		    }
		    else {
		        if(set.isEmpty()) {
		            if(x == 1) io.write(a[r+1] + "\n");
		            else io.write(a[1] + "\n");
		        }
		        else {
		            io.write(set.first() + "\n");
		        }
		    }
		}

		io.close();

	}

}
```
