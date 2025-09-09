```java

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
	static char[][] arr;
	static int[][] dp;
	static int width,height,goalY,goalX , curY,curX, curCnt,curDir,ans;
	static boolean success = false;
	
	static Queue<Point> q = new LinkedList<>();
	static int[] dy = {-1,0,1,0};
	static int[] dx = {0,1,0,-1};
	
	static final char WALL = '*';
	static final char GOAL = 'C';

	
	static class Point{
		int y,x,dir;
		
		public Point(int y,int x,int dir) {
			this.y = y;
			this.x = x;
			this.dir = dir;
		}
	}
    
    public static void main(String[] args) throws NumberFormatException, IOException {
		init();
		process();
		print();
    }
    
    public static void init() throws NumberFormatException, IOException {
    	BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    	StringTokenizer st = new StringTokenizer(br.readLine());
    	width = Integer.parseInt(st.nextToken());
    	height = Integer.parseInt(st.nextToken());
    	arr = new char[height][width];
    	dp = new int[height][width];
    	boolean first = true;
    	
    	for (int i = 0 ; i < height; i++) {
    		String input = br.readLine();
    		arr[i] = input.toCharArray();
    		Arrays.fill(dp[i], Integer.MAX_VALUE/2);
    		for (int j = 0; j < width; j++) {
    			if (arr[i][j] == GOAL && first) {
    				first = false;
    				dp[i][j] = -1;
    				for (int k = 0; k < 4; k++) q.add(new Point(i,j,k));
    			} else if (arr[i][j] == GOAL) {
    				goalY = i;
    				goalX = j;
    			} else if (arr[i][j] == WALL) {
    				dp[i][j] = -1;
    			}
    		}
    	}
    	
    }
    
    public static void process() { 	
    	while(!q.isEmpty()) {
    		int qLen = q.size();
    		for (int i = 0; i < qLen; i++) {
    			unitProcess();
    		}
    	}
    }
    
    
    public static void unitProcess() {
		Point p = q.poll();
		for (int j = 0; j < 4; j++) {
			curY = p.y;
			curX = p.x;
			curDir = j;
			curCnt = dp[curY][curX] +1 ;
			if (curDir == p.dir) continue;
			
			while(true) {
				curY += dy[curDir];
				curX += dx[curDir];
				if (curY == goalY && curX == goalX) {
					ans = curCnt;
				}
				
				if (curY >= height || curY < 0 || curX >= width || curX < 0 ) break;
				if (arr[curY][curX] == WALL) break;
				if (dp[curY][curX] <= curCnt) continue;
				
				dp[curY][curX] = curCnt;
				q.add(new Point(curY,curX,j));
				
				
				
			}
			
		}
    }

    public static void print() {
    	System.out.println(dp[goalY][goalX]);
    }
}
```
