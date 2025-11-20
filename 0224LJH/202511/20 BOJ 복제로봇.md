```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.HashMap;
import java.util.HashSet;
import java.util.LinkedList;
import java.util.PriorityQueue;
import java.util.Queue;
import java.util.StringTokenizer;

public class Main {
	
	// 각 s,k에서 모두 bfs를 진행하여 거리표 만들고. MST. 끝
	
	static char WALL = '1';
	static char EMPTY = '0';
	static char START = 'S';
	static char KEY = 'K';
	static int[] dy = {-1,0,1,0};
	static int[] dx = {0,1,0,-1};
	
	static class Box{
		int y,x,num;
		char type;
		
		public Box (int y, int x, char c, int idx) {
			this.y = y;
			this.x = x;
			this.num = idx;
			this.type = c;
		}
		
	}
	
	static class Edge implements Comparable<Edge>{
		Box from;
		Box to;
		int dis;
		
		public Edge(Box from, Box to, int dis) {
			this.from = from;
			this.to = to;
			this.dis = dis;
		}
		
		@Override
		public int compareTo(Edge e) {
			return Integer.compare(this.dis, e.dis);
		}
	}
	
	
	static Box[][] arr;
	static Box[] point;
	static int[] parent;
	static int size,keyCnt,boxCnt,ans;
	
	static PriorityQueue<Edge> pq = new PriorityQueue<>();

	
    public static void main(String[] args) throws IOException {
    	init();
    	process();
    	print();

    	
    }
    
    private static void init() throws IOException{
    	BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    	StringTokenizer st = new StringTokenizer(br.readLine());
    	size = Integer.parseInt(st.nextToken());
    	keyCnt = Integer.parseInt(st.nextToken());
    	
    	ans = 0;
    	arr = new Box[size][size];
    	point = new Box[size*size];
    	parent = new int[size*size];
    	boxCnt = 0;
    	
    	for (int i = 0; i < size; i++) {
    		char[] cArr= br.readLine().toCharArray();
    		for (int j = 0; j < size; j++) {
    			arr[i][j] = new Box(i,j,cArr[j],boxCnt);
    			if (arr[i][j].type == START || arr[i][j].type == KEY) {
    				point[boxCnt++] = arr[i][j];
    			}
    			
    		}
    	}
    	
    	for (int i = 0; i < size*size; i++) {
    		parent[i] = i;
    	}


    }
    
    private static void process() throws IOException {
    	getEdge();
    	getDis();
    	check();

    }
    
    private static void check() {
    	for (int i= 0; i < boxCnt; i++) {
    		if ( find(i) != 0) {
    			ans = -1;
    			return;
    		}
    	}
    }
    
    private static void getDis() {
 
    	while(!pq.isEmpty()) {
    		Edge e = pq.poll();
    		union(e.from.num, e.to.num, e.dis);
    	
    	}
    }
    
    private static int find(int idx) {
    	if (parent[idx] == idx) return idx;
    	
    	return parent[idx] = find(parent[idx]);
    }
    
    private static void union(int idx1, int idx2,int dis) {
    	int root1 = find(idx1);
    	int root2 = find(idx2);
    	
    	if (root1 == root2) return;
    	
    	if (root1 < root2) {
    		parent[root2] = root1;
    	} else {
    		parent[root1] = root2;
    	}
    	ans += dis;
    	
    	return;
    }
    
    
    private static void getEdge() {
    	
    	for (int i = 0; i < boxCnt; i++) {
    		boolean[][] visited = new boolean[size][size];
    		
    		Box box = point[i];
    		
    		Queue<Box> q = new LinkedList<>();
    		
    		q.add(box);
    		visited[box.y][box.x] = true;
    		
    		
    		int dis = 0;
    		
    		while(!q.isEmpty()) {
    			dis++;
    			int cnt = q.size();
    			for (int j = 0; j < cnt; j++) {
        			Box b = q.poll();
        			int y = b.y;
        			int x = b.x;
        			
        			
        			
        			for (int k = 0; k < 4; k++) {
        				int ny = y + dy[k];
        				int nx = x + dx[k];
        				
        				if ( ny < 0 || nx < 0 || ny >= size || nx >= size) continue;
        				if ( visited[ny][nx] ) continue;
        				if (arr[ny][nx].type == WALL) continue;
        				
        				visited[ny][nx] = true;
        				
        				if (arr[ny][nx].type != EMPTY) {
        					Edge e = new Edge(box,arr[ny][nx],dis);
        					pq.add(e);
        				}
        				
        				q.add(arr[ny][nx]);
        			}
    			}

    			
    			
    		}
    	}
    }

	private static void print() {
		System.out.println(ans);
    }

}
```
