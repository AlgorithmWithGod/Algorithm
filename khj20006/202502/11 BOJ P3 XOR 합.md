```java

import java.util.*;
import java.io.*;

class Node{
	int d;
	Node l, r;
	Node(int d){this.d = d;}
}

class Trie{
	Node root;
	Trie(){root = new Node(31);}
	void insert(int x) {
		Node now = root;
		for(int i=30;i>=0;i--) {
			int bit = x & (1<<i);
			x -= bit;
			if(bit == 0) {
				if(now.l == null) now.l = new Node(i);
				now = now.l;
			}
			else {
				if(now.r == null) now.r = new Node(i);
				now = now.r;
			}
		}
	}
	// x 와 xor했을 때 가장 큰 값 찾기
	int find(int x) {
		Node now = root;
		int res = 0;
		for(int i=30;i>=0;i--) {
			int bit = x & (1<<i);
			if(bit != 0) {
				if(now.l == null) now = now.r;
				else {
					res += (1<<i);
					now = now.l;
				}
			}
			else {
				if(now.r == null) now = now.l;
				else {
					res += (1<<i);
					now = now.r;
				}
			}
		}
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
	static int T, N;
	static int[] S;
	
	
	public static void main(String[] args) throws Exception {
		
		ready();
		//solve();
	
		bwEnd();
	}
	
	static void ready() throws Exception{

		T = Integer.parseInt(br.readLine());
		while(T-- > 0) {
			trie = new Trie();
			
			N = Integer.parseInt(br.readLine());
			S = new int[N+1];

			nextLine();
			for(int i=1;i<=N;i++) {
				S[i] = nextInt();
				S[i] ^= S[i-1];
			}
			solve();
		}
		
	}
	
	static void solve() throws Exception{
		
		for(int i=1;i<=N;i++) trie.insert(S[i]);
		
		int ans = 0;
		for(int i=0;i<N;i++) ans = Math.max(ans, trie.find(S[i]));
		bw.write(ans+"\n");
		
	}
	
	
}

```
