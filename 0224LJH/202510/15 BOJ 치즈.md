```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;
import java.awt.Point;

public class Main {
	
	static int height, width, round,ans;
	static int[][] arr;
	static Queue<Point> cheeses = new LinkedList<>();
	
	static int[] dy = { -1,0,1,0};
	static int[] dx = { 0,1,0,-1};
	
	static final int OUTSIDE = 0;
	static final int CHEESE = 1;
	static final int INSIDE = 2;

    
    public static void main(String[] args) throws NumberFormatException, IOException {
    	init();
    	process();
    	print();
    }
    

    
    public static void init() throws NumberFormatException, IOException {
    	BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    	StringTokenizer st = new StringTokenizer(br.readLine());
    	height = Integer.parseInt(st.nextToken());
    	width = Integer.parseInt(st.nextToken());
    	arr = new int[height][width];
    	
    	for (int i = 0; i < height; i++) {
    		st = new StringTokenizer(br.readLine());
    		for (int j = 0; j < width; j++) {
    			arr[i][j] = Integer.parseInt(st.nextToken());
    		}
    	}
    	
	}
    
    public static void process() throws IOException { 	

    	findInside();
    	int second = 0;
    	while (!cheeses.isEmpty()) {
    		melt();
    		second++;
    	}
    	

    	ans = second;
    }
    
    private static void melt() {
    	Queue<Point> cheeseLeft = new LinkedList<>();
    	Queue<Point> deleteQ = new LinkedList<>();
    	
    	while(!cheeses.isEmpty()) {
    		Point p = cheeses.poll();
    		
    		if(isNotMelting(p.y , p.x)) {
    			cheeseLeft.add(p);
    			continue;
    		}
    		deleteQ.add(p);
    	}
    	
    	while(!deleteQ.isEmpty()) {
    		Point p = deleteQ.poll();

    		arr[p.y][p.x] = OUTSIDE;
    		
    		for (int i = 0; i <4 ; i++) {
    			int ny = p.y + dy[i];
    			int nx = p.x + dx[i];
    			if ( ny < 0 || nx < 0 || ny >= height || nx >= width 
    					|| arr[ny][nx] == CHEESE || arr[ny][nx] == OUTSIDE) continue;
    			
    			arr[ny][nx] = OUTSIDE;
    			Point nPoint = new Point(nx,ny); 
    			
    			Queue<Point> insideCheese = new LinkedList<>();
    			
    			insideCheese.add(nPoint);
    			while(!insideCheese.isEmpty()) {
    				Point iP =insideCheese.poll();
    				for (int j = 0; j < 4; j++) {
    					int nIy = iP.y + dy[j];
    					int nIx = iP.x + dx[j];
    					if ( nIy < 0 || nIx < 0 || nIy >= height || nIx >= width 
    	    					|| arr[nIy][nIx] == CHEESE || arr[nIy][nIx] == OUTSIDE) continue;
    					
    					arr[nIy][nIx] = OUTSIDE;
    					insideCheese.add(new Point(nIx, nIy));
    				}
    			}
    		}
    	}
    	
    	cheeses = cheeseLeft;
    	
    	
    }
    private static boolean isNotMelting(int y,int x) {
    	
    	int outSideCnt = 0;
    	
    	for (int i = 0 ; i < 4; i++) {
			int ny = y + dy[i];
			int nx = x + dx[i];
			if ( ny < 0 || nx < 0 || ny >= height || nx >= width || arr[ny][nx] == OUTSIDE) outSideCnt++;
    	}
//    	System.out.println(y  + " " + x + " -> "+ outSideCnt);
    	
    	return (outSideCnt < 2) ;
    }
    
    private static void findInside() {
    	boolean[][] visited = new boolean[height][width];
    	
    	for (int i = 0; i < height; i++) {
    		for (int j = 0; j < width; j++) {
    			if (visited[i][j] ) continue;
    			if (arr[i][j] == CHEESE) {
    				cheeses.add(new Point(j,i));
    				continue;
    			}
    			
    			Queue<Point> q = new LinkedList<>();
    			Set<Point> set = new HashSet<>();
    			
    			Point start = new Point(j,i);
    			boolean isInside = true;
    			q.add(start);
    			set.add(start);
    			
    			while(!q.isEmpty()) {
    				Point p = q.poll();
    				
    				for (int k = 0; k <4 ; k++) {
    					int ny = p.y + dy[k];
    					int nx = p.x + dx[k];
    					
    					if ( ny < 0 || nx < 0 || ny >= height || nx >= width) {
    						// 밖으로 벗어남 -> 치즈안이 아님
    						isInside = false;
    						continue;
    					}
    					
    					if (visited[ny][nx] || arr[ny][nx] == CHEESE) continue;
    					
    					Point np = new Point(nx, ny);
    					q.add(np);
    					set.add(np);
    					visited[ny][nx] = true;
    					
    				}
    			}
    			
    			for (Point p:set) {
    				arr[p.y][p.x] = (isInside)?2:0; 
    			}
    			
    		}
    	}
    }
    



	public static void print() {
		System.out.println(ans);

    }
}
```
