
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
	
	static final char LEFT = 'L'; // 감소 
	static final char RIGHT = 'R'; // 증가
	static ArrayList<Line> lines = new ArrayList<>();
	
	static int[] dy = {0,-1,0,1};
	static int[] dx = {1,0,-1,0};
	
	static int maxLimit,minLimit,turnCnt,curDir,curX,curY;
	static long curTime;
	static Turn[] turns;
	
	static class Turn{
		int after;
		char dir;
		
		public Turn(int after, String dir) {
			this.after = after;
			this.dir = dir.charAt(0);
		}
	}
	
	static class Line{
		int stX, stY, endX, endY;
		boolean isVertical;
		
		public Line(int stX, int stY, int endX, int endY) {

			isVertical = (stX == endX);
			if (isVertical) {
				this.stX = this.endX = stX;
				this.stY = Math.min(stY, endY);
				this.endY = Math.max(stY, endY);
			} else {
				this.stY = this.endY = stY;
				this.stX = Math.min(stX, endX);
				this.endX = Math.max(stX, endX);
			}
		}
		
		public boolean check(Line l) {
			// 둘이 크로스되는지, 아니면 평행한지 부터 판단
			if (this.isVertical && l.isVertical) {
				if (this.stX != l.stX) return true;
				if (this.stY > l.endY || this.endY < l.stY) return true; 
				return false;
			} else if (!this.isVertical && !l.isVertical){
				if (this.stY != l.stY) return true;
				if (this.stX > l.endX || this.endX < l.stX) return true;
				return false;
			}else {
				if (!this.isVertical) {
					if((this.stY >= l.stY && this.stY <= l.endY)&&
							(l.stX >= this.stX && l.stX <= this.endX))return false;
					return true;
				} else {
					if((l.stY >= this.stY && l.stY <= this.endY)&&
							(this.stX >= l.stX && this.stX <= l.endX))return false;
					return true;
				}
			}
			
		}
	}

	

	
    
    public static void main(String[] args) throws NumberFormatException, IOException {
		init();
		process();
		print();
    }
    
    public static void init() throws NumberFormatException, IOException {
    	BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    	maxLimit = Integer.parseInt(br.readLine());
    	minLimit = maxLimit*(-1);
    	turnCnt = Integer.parseInt(br.readLine());
    	turns = new Turn[turnCnt+1];
    	curDir = 0;
    	curTime = 0;
    	curY = 0;
    	curX = 0;
    	
    	for (int i = 0; i < turnCnt; i++) {
    		StringTokenizer st = new StringTokenizer(br.readLine());
    		int after = Integer.parseInt(st.nextToken());
    		String dir = st.nextToken();
    		turns[i] = new Turn(after,dir);
    	}
    	
 


    	
    }
    
    public static void process() { 	
    	lines.add(new Line(minLimit, minLimit-1, maxLimit, minLimit-1));
    	lines.add(new Line(minLimit-1, minLimit, minLimit-1, maxLimit));
    	lines.add(new Line(maxLimit+1, minLimit, maxLimit+1, maxLimit));
    	lines.add(new Line(minLimit, maxLimit+1, maxLimit, maxLimit+1));
    	
    	turns[turnCnt] = new Turn(1000000000,"L");
    	
    	
    	for(int i = 0 ; i <= turnCnt; i++) {
    		Turn t = turns[i];
    		int nX = curX + dx[curDir] * t.after;
    		int nY = curY + dy[curDir] * t.after;
    		int minTime = Integer.MAX_VALUE;
    		boolean isOkay = true;
    		
    		
    		Line nLine = new Line(curX, curY, nX, nY);
    		
    		for (Line l: lines) {
    			
    			if(!l.check(nLine)) {
    				int tempMin = Integer.MAX_VALUE;
    				
    				if(curDir == 0) tempMin = Math.min(tempMin, l.stX - curX);
    				if(curDir == 1) tempMin = Math.min(tempMin,  curY - l.endY);
    				if(curDir == 2) tempMin = Math.min(tempMin, curX - l.endX);
    				if(curDir == 3) tempMin = Math.min(tempMin, l.stY - curY);
    				
    				
    				if (tempMin == 0) continue;
    				isOkay = false;
    				minTime = Math.min(minTime, tempMin);
    			}
    		}
    		
    		lines.add(nLine);
    		
    		
    		if (isOkay) {
    			curTime += t.after;
    			if (t.dir == LEFT) curDir = (curDir +3)%4;
    			else curDir = (curDir+1)%4;
    			
    			curX = nX;
    			curY = nY;
    		} else {
    			curTime += minTime;
    			return;
    		}
    		
    	}

    }




	public static void print() {
		System.out.println(curTime);
    }
}
