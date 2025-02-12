```java

import java.util.*;
import java.io.*;

class Node{
	Node[] next;
	int cnt;
	Node(){
		next = new Node[26];
		cnt = 0;
	}
}

class Trie{
	Node root;
	Trie(){
		root = new Node();
	}
	void insert(String str) {
		Node now = root;
		for(char i:str.toCharArray()) {
			if(now.next[i-'a'] == null) now.next[i-'a'] = new Node();
			now = now.next[i-'a'];
			now.cnt++;
		}
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
	static long[][] count;
	static long[] dp;
	static long mod = (long)1e9 + 7;
	static String S;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
	}
	
	static void ready() throws Exception{

		trie = new Trie();
		N = Integer.parseInt(br.readLine());
		for(int i=0;i<N;i++) trie.insert(br.readLine());
		
		S = br.readLine();
		dp = new long[S.length()+1];
		count = new long[S.length()+1][301];

	}
	
	static void solve() throws Exception{

		for(int i=1;i<=S.length();i++) {
			
			Node now = trie.root;
			// i로 시작하는 문자열, 길이 300까지만
			for(int j=1;i+j-2<S.length();j++) {
				// count[i+j-1][j]
				
				int x = S.charAt(i+j-2)-'a';
				if(now.next[x] == null) break;
				now = now.next[x];
				count[i+j-1][j] = now.cnt;
				
			}
		}
		
		dp[0] = 1;
		for(int i=1;i<=S.length();i++) for(int j=1;j<=Math.min(300, i);j++) {
			dp[i] += (dp[i-j] * count[i][j]);
			dp[i] %= mod;
		}
		bw.write(dp[S.length()]+"\n");
		
	}
	
	
}

```
