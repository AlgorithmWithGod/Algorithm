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

	static int N, M;
	static int[] next, root, indeg;
	static long[] cnt, origin;
	static List<List<Integer>> cycles;
	static boolean[] isCycle;

	static int f(int x) {return x==root[x] ? x : (root[x]=f(root[x]));}

	public static void main(String[] args) throws Exception {

		io = new IOController();

		N = io.nextInt();
		M = io.nextInt();
		next = new int[M];
		origin = new long[M];
		root = new int[M];
		cnt = new long[M];
		indeg = new int[M];
		for(int i=0;i<M;i++) root[i] = i;
		for(int i=0;i<M;i++) {
			next[i] = (i*2)%M;
			indeg[next[i]]++;
			int x = f(i), y = f(next[i]);
			if(x != y) root[x] = y;
		}
		for(int i=0;i<N;i++) cnt[io.nextInt()]++;

		cycles = new ArrayList<>();
		boolean[] vis = new boolean[M];
		boolean[] vvis = new boolean[M];
		int[] par = new int[M];
		for(int i=0;i<M;i++) if(!vis[f(i)]) {
			vis[f(i)] = true;
			int n = i;
			vvis[n] = true;
			while(!vvis[next[n]]) {
				par[next[n]] = n;
				n = next[n];
				vvis[n] = true;
			}
			List<Integer> list = new ArrayList<>();
			int r = next[n];
			list.add(r);
			while(n != r) {
				list.add(n);
				n = par[n];
			}
			cycles.add(list);
		}

		isCycle = new boolean[M];
		for(List<Integer> list : cycles) {
			for(int i:list) isCycle[i] = true;
		}

		Queue<Integer> q = new ArrayDeque<>();
		for(int i=0;i<M;i++) if(indeg[i] == 0) q.add(i);
		while(!q.isEmpty()) {
			int n = q.poll();
			origin[next[n]] += origin[n] + cnt[n];
			cnt[next[n]] += cnt[n];
			if(!isCycle[next[n]]) {
				if(--indeg[next[n]] == 0) q.add(next[n]);
			}
		}

		long ans = Long.MAX_VALUE, S = 0;
		for(List<Integer> list : cycles) {
			long sum = 0, s = 0;
			int zeroCnt = 0;
			for(int i=0;i<list.size();i++) {
				if(cnt[list.get(i)] == 0) zeroCnt++;
				sum += (long)i * cnt[list.get(i)];
				s += cnt[list.get(i)];
			}
			if(s < S) continue;

			if(zeroCnt == list.size()-1) {
				int nonzeroNum = 0;
				for(int i:list) if(cnt[i] != 0) nonzeroNum = i;

				long res = Long.MAX_VALUE;
				for(int i=0;i<M;i++) if(f(i) == f(nonzeroNum)) {
					if(cnt[i] == s) res = Math.min(res, origin[i]);
				}

				if(s > S) ans = res;
				else ans = Math.min(ans, res);
				S = s;
				continue;
			}

			long res = sum;
			for(int i=0;i<list.size()-1;i++) {
				sum += (long)list.size() * cnt[list.get(i)] - s;
				res = Math.min(res, sum);
			}

			long orgsum = 0;
			for(int i:list) {
				orgsum += origin[i];
			}
			res += orgsum;

			if(s > S) ans = res;
			else ans = Math.min(ans, res);
			S = s;
		}

		io.write(S + " " + ans + "\n");

		io.close();

	}

}
```
