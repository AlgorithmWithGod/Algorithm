```java
import java.util.*;
import java.io.*;

class Solution
{
	static int[][] dir = new int[][] {{1,0},{0,1},{1,1},{-1,1}};
	static int[][] board = new int[19][19];
	static Point answer = new Point(-1,-1,-1);
	
    public static void main(String[] args) throws Exception{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
	    
	    for (int i = 0; i < 19; i++) {
	    	st = new StringTokenizer(br.readLine());
	    	for (int j = 0; j < 19; j++) {
	    		board[i][j] = Integer.parseInt(st.nextToken());
	    	}
	    }

	    for (int i = 0; i <19; i++) {
	    	for (int j = 0; j < 19; j++) {
	    		if (board[i][j] == 1 || board[i][j] == 2) {
	    			check(i, j, board[i][j]);
	    		}
	    	}
	    }
	    if (answer.x == -1) System.out.println(0);
	    else {
	    	System.out.println(answer.type);
		    System.out.println(answer.y + " " + answer.x);
	    }
    }
    
    public static void check(int y, int x, int type) {
    	for (int[] d : dir) {
    		int cnt = 1;
    		int ny = y + d[0];
    		int nx = x + d[1];
    		
    		while (ny >= 0 && ny < 19 && nx >= 0 && nx < 19 && board[ny][nx] == type) {
    			cnt += 1;
    			ny += d[0];
    			nx += d[1];
    		}
    		if (cnt == 5) {
    			if (y-d[0] >= 0 && x-d[1] >= 0 && y-d[0] < 19 && board[y-d[0]][x-d[1]] == type) continue; 
    			answer = new Point(y+1, x+1, type);
    		}
    	}
    }
    
    static class Point {
    	int y;
    	int x;
    	int type;
    	public Point(int y, int x, int type) {
    		this.y = y;
    		this.x = x;
    		this.type = type;
    	}
    }
}

```
