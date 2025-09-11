```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
	static int height, width, ans;
	static int[][] arr;
	static boolean[][] visited;
	static boolean isTop;

	static int[] dy = {-1,-1,0,1,1,1,0,-1};
	static int[] dx = {0,1,1,1,0,-1,-1,-1};

    
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
    	visited = new boolean[height][width];
    	
    	for (int i = 0; i < height; i++) {
    		st = new StringTokenizer(br.readLine());
    		for (int j = 0; j < width; j++) {
    			arr[i][j] =Integer.parseInt(st.nextToken());
    		}
    	}
    }
    
    public static void process() {    
    	for (int i = 0; i < height; i++) {
    		for (int j = 0; j < width; j++) {
    			if (!visited[i][j]) {
    				isTop = true;
    				check(i,j);
    				if (isTop) ans++;
    			}
    		}
    	}

    }
    
    public static void check(int y, int x) {
    	int num = arr[y][x];
    	visited[y][x] = true;
    	for (int i = 0; i < 8; i++) {
    		int ny = dy[i] + y;
    		int nx = dx[i] + x;
    		if (ny < 0 || nx < 0 || ny >= height || nx >= width) continue;
    		
    		int nNum = arr[ny][nx];
    		
    		if (nNum < num) continue;
    		else if (nNum == num ) {
    			if (!visited[ny][nx])check(ny,nx);
    		}
    		else {
    			isTop = false;
    			continue;
    		}
    	}
    }

    


    public static void print() {
       System.out.println(ans);
    }
}
```
