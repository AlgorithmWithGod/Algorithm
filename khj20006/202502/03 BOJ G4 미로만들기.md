```java

import java.util.*;
import java.io.*;

class Node{
	int x, y, c;
	Node(int x, int y, int c){
		this.x = x;
		this.y = y;
		this.c = c;
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

	public static void main(String[] args) throws Exception {
		
		int[] dx = {1,0,-1,0};
		int[] dy = {0,1,0,-1};

		nextLine();
		int N = nextInt();
		char[][] arr = new char[N][N];
		
		for(int i=0;i<N;i++) {
			String line = br.readLine();
			for(int j=0;j<N;j++) arr[i][j] = line.charAt(j);
		}
		
		Deque<Node> Q = new ArrayDeque<>();
		boolean[][] vis = new boolean[N][N];
		vis[0][0] = true;
		Q.offerFirst(new Node(0,0,0));
		
		while(!Q.isEmpty()) {
			
			Node now = Q.pollFirst();
			if(now.x == N-1 && now.y == N-1) {
				bw.write(now.c + "\n");
				bwEnd();
				return;
			}
			
			for(int i=0;i<4;i++) {
				int x = now.x + dx[i], y = now.y + dy[i];
				if(x<0 || x>=N || y<0 || y>=N || vis[x][y]) continue;
				vis[x][y] = true;
				if(arr[x][y] == '0') Q.offerLast(new Node(x,y,now.c+1));
				else Q.offerFirst(new Node(x,y,now.c));
			}
			
		}
		
		bwEnd();
	}

}

```
