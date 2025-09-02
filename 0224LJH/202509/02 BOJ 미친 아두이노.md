```java
import java.io.IOException;
import java.math.BigInteger;
import java.awt.Point;
import java.io.*;
import java.util.*;


public class Main {
	
	static int height,width,len,nTargetY,nTargetX,res;
	
	static int[] dy = {0,1,1,1,0,0,0,-1,-1,-1};
	static int[] dx = {0,-1,0,1,-1,0,1,-1,0,1};
	static int[] dir;
	
	static Point target;
	static Queue<Arduino> arduinos;
	static Arduino[][] visited;
	static StringBuilder sb = new StringBuilder();
	
	static class Arduino{
		Point p;
		boolean isOkay;
		
		public Arduino (int x, int y){
			p = new Point(x,y);
			isOkay = true;
		}
		
	}

	public static void main(String[] args) throws IOException {
		init();
		process();
		print();
		
	}
	
	public static void init() throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		
		height = Integer.parseInt(st.nextToken());
		width = Integer.parseInt(st.nextToken());
		arduinos = new LinkedList<>();
		
		for (int i = 0; i < height; i++) {
			String[] input = br.readLine().split("");
			for (int j = 0; j < width; j++) {
				String temp = input[j];
				
				if (temp.equals("I")) target = new Point(j,i);
				else if (temp.equals("R")) arduinos.add(new Arduino(j,i));
			}
		}
		
		String[] rawNum = br.readLine().split("");
		len = rawNum.length;
		dir = new int[len];
		for (int i = 0; i < len; i++) dir[i] = Integer.parseInt(rawNum[i]);
		
	}

	public static void process() throws IOException {
		
		res = -1; // -1이 유지되면 끝까지 이동한것.
		
		for (int i = 0; i < len; i++) {
			visited = new Arduino [height][width];
			nTargetY = target.y + dy[dir[i]];
			nTargetX = target.x + dx[dir[i]];
			
			target = new Point(nTargetX,nTargetY);
			
			processEach(i+1);
			
			if (res != -1) break;

		}
		
		
		makeAns();
	}
	


	private static void processEach(int round) {
		int qSize = arduinos.size();
		
		for (int j = 0 ; j < qSize; j++) {
			Arduino a = arduinos.poll();
			
			if (!a.isOkay) continue;
			
			int ny = a.p.y;
			int nx = a.p.x;
			
			if (a.p.y != nTargetY) ny += a.p.y < nTargetY?(1):(-1);
			if (a.p.x != nTargetX) nx += a.p.x < nTargetX?(1):(-1);
			
			a.p.y = ny;
			a.p.x = nx;
			
			if (ny == nTargetY && nx == nTargetX) {
				res = round;
				break;
			}
			
			if (visited[ny][nx] == null) {
				visited[ny][nx] = a;
				arduinos.add(a);
			} else {
				visited[ny][nx].isOkay = false;
			}
		}
	}
	
	private static void makeAns() {
		if (res != -1) {
			sb.append("kraj ").append(res).append("\n");
			return;
		}
		
		String[][] ansArr = new String[height][width];
		
		for (int i = 0; i < height; i++) Arrays.fill(ansArr[i], ".");
		
		ansArr[target.y][target.x] = "I";
		
		while(!arduinos.isEmpty()) {
			Arduino a = arduinos.poll();
			if (!a.isOkay) continue;
			
			ansArr[a.p.y][a.p.x] = "R";
		}
		
		for (int i = 0; i < height; i++) {
			for (int j = 0; j <width; j++) {
				sb.append(ansArr[i][j]);
			}
			sb.append("\n");
		}
		
	}

	public static void print() {
		System.out.print(sb.toString());
	}
}

```
