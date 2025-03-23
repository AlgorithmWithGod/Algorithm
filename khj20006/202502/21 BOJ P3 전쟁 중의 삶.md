```java

import java.util.*;
import java.io.*;

class Node{
	int cnt;
	Node l, r;
	Node(){ cnt = 0; }
}

class Trie{
	Node root;
	Trie(){ root = new Node(); }
	
	void insert(long x) {
		
		Stack<Integer> S = new Stack<>();
		while(x > 0) {
			if((x&1) == 0) S.add(0);
			else S.add(1);
			x >>= 1;
		}
		
		Node now = root;
		while(!S.isEmpty()) {
			int a = S.pop();
			if(a == 0) {
				if(now.l == null) now.l = new Node();
				now = now.l;
				now.cnt++;
			}
			else {
				if(now.r == null) now.r = new Node();
				now = now.r;
				now.cnt++;
			}
		}
	}
	
	int DFS(int v) {
		Node now = root;
		int ans = 1;
		if(now.l != null) ans += dfs(now.l, v);
		if(now.r != null) ans += dfs(now.r, v);
		return ans;
	}
	
	int dfs(Node now, int v) {
		int res = now.cnt == v ? 0 : 1;
		if(now.l != null) res += dfs(now.l, v);
		if(now.r != null) res += dfs(now.r, v);
		return res;
	}
}

class Main {
	
	// IO field
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
	static StringTokenizer st;

	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	static long nextLong() {return Long.parseLong(st.nextToken());}
	static void bwEnd() throws Exception {bw.flush();bw.close();}
	
	// Additional field
	
	static Trie trie;
	static int N;
	
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		trie = new Trie();
		
		N = Integer.parseInt(br.readLine());
		nextLine();
		for(int i=0;i<N;i++) {
			long a = nextLong();
			trie.insert(a);
		}		
		
	}
	
	static void solve() throws Exception{

		bw.write(trie.DFS(N)+"\n");
		
	}
	
}

```
