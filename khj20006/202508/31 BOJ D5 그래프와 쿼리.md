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

class DisjointSet {
	int size;
	int[] root, rank;
	Stack<int[]> works;

	DisjointSet(int size) {
		this.size = size;
		root = new int[size+1];
		rank = new int[size+1];
		for(int i=1;i<=size;i++) {
			root[i] = i;
			rank[i] = 1;
		}
		works = new Stack<>();
	}

	int find(int x) { return x == root[x] ? x : find(root[x]); }

	void union(int a, int b) {
		int x = find(a), y = find(b);
		if(x == y) {
			works.push(new int[]{-1,-1,-1});
			return;
		}
		if(rank[x] < rank[y]) {
			rank[y] += rank[x];
			root[x] = y;
			works.add(new int[]{x, y, rank[x]});
		}
		else {
			rank[x] += rank[y];
			root[y] = x;
			works.add(new int[]{y, x, rank[y]});
		}
	}

	void rollback() {
		if (!works.isEmpty()) {
			int[] last = works.pop();
			int x = last[0], y = last[1], r = last[2];
			if(x == -1) return;
			rank[y] -= r;
			root[x] = x;
		}
	}

}

public class Main {

	static IOController io;

	//

	static int N, M;
	static List<int[]>[] lists;
	static DisjointSet ds;
	static List<int[]>[] needAnswer;

	static void update(int s, int e, int l, int r, int n, int a, int b) {
		if(l>r || l>e || r<s) return;
		if(l<=s && e<=r) {
			lists[n].add(new int[]{a,b});
			return;
		}
		int m = (s+e)>>1;
		update(s,m,l,r,n*2,a,b);
		update(m+1,e,l,r,n*2+1,a,b);
	}

	static void clear(int s, int e, int n) throws Exception {
		for(int[] edge : lists[n]) {
			int a = edge[0], b = edge[1];
			ds.union(a,b);
		}
		if(s == e) {
			for(int[] info : needAnswer[s]) {
				int a = info[0], b = info[1];
				if(ds.find(a) == ds.find(b)) io.write("1\n");
				else io.write("0\n");
			}
			for(int i=0;i<lists[n].size();i++) ds.rollback();
			return;
		}
		int m = (s+e)>>1;
		clear(s,m,n*2);
		clear(m+1,e,n*2+1);
		for(int i=0;i<lists[n].size();i++) ds.rollback();
	}

	public static void main(String[] args) throws Exception {

		io = new IOController();

		N = io.nextInt();
		M = io.nextInt();
		lists = new List[M*4];
		for(int i=0;i<M*4;i++) lists[i] = new ArrayList<>();
		ds = new DisjointSet(N);
		needAnswer = new List[M];
		for(int i=0;i<M;i++) needAnswer[i] = new ArrayList<>();
		Map<String, Integer> map = new TreeMap<>();
		for(int i=0;i<M;i++) {
			int op = io.nextInt();
			int a = io.nextInt();
			int b = io.nextInt();
			if(a > b) {
				int t = a;
				a = b;
				b = t;
			}
			if(op == 1) map.put(a+","+b, i);
			else if(op == 2) {
				update(0,M-1,map.get(a+","+b),i,1,a,b);
				map.remove(a+","+b);
			}
			else {
				needAnswer[i].add(new int[]{a,b});
			}
		}
		for(String key : map.keySet()) {
			String[] words = key.split(",");
			int a = Integer.parseInt(words[0]);
			int b = Integer.parseInt(words[1]);
			update(0,M-1,map.get(key),M,1,a,b);
		}

		clear(0,M-1,1);

		io.close();

	}

}
```
