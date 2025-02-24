```java

import java.util.*;
import java.io.*;

class Node{
	int attacks = 0;
	int mine = 0;
	Node(int attacks, int mine){
		this.attacks = attacks;
		this.mine = mine;
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

	static int N, K;
	static int[] A;
	static String command;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{

		N = Integer.parseInt(br.readLine());
		A = new int[N+2];
		nextLine();
		for(int i=1;i<=N;i++) A[i] = nextInt();
		K = Integer.parseInt(br.readLine());
		command = br.readLine();
		
	}
	
	static void solve() throws Exception{

		int idx = 0, cur = 1;
		while(idx < command.length()) {
			if(command.charAt(idx) == 'J') {
				idx++;
				if(A[cur+1] != 0) {
					bw.write("NO");
					return;
				}
				cur++;
				break;
			}
			if(command.charAt(idx) == 'D') {
				if(A[cur+1] <= -1) A[cur+1] = 0;
			}
			else {
				if(A[cur+1] == -1) {
					bw.write("NO");
					return;
				}
				A[cur+1] = Math.max(0, A[cur+1] - 1);
			}
			idx++;
		}
		if(cur == 1) {
			bw.write("NO");
			return;
		}
		
		int atts = 0, mine = 0;
		List<Node> L = new ArrayList<>();
		for(int i=idx;i<idx+K;i++) {
			if(command.charAt(i%K) == 'J') {
				L.add(new Node(atts, mine));
				atts = 0;
				mine = 0;
			}
			else if(command.charAt(i%K) == 'D') {
				if(atts == 0) mine = 1;
			}
			else {
				atts++;
			}
		}
		
		
		idx = 0;
		while(cur < N) {
			Node now = L.get(idx%L.size());
			if(A[cur+1] == -1) {
				if(now.mine == 0) {
					bw.write("NO");
					return;
				}
			}
			else {
				if(now.attacks < A[cur+1]) {
					bw.write("NO");
					return;
				}
			}
			A[cur+1] = 0;
			cur++;
			idx++;
		}
		bw.write("YES");
		
	}
	
}

```
