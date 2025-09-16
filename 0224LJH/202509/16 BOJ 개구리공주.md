```java

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {

	
	static HashMap<Integer,TreeSet<Plant>> sumMap = new HashMap<>(); // X+Y가 같은 애들끼리. 여기선 차이가 줄 기준
	static HashMap<Integer,TreeSet<Plant>> diffMap = new HashMap<>();// X-Y가 같은 애들끼리. 여기선 합이 클수록 뒤.
	static Plant[] plants;
	static int[] dy = {1,-1,1,-1};
	static int[] dx = {1,1,-1,-1};
	static int[] jumpDir; // 한글자 받아서 -'A'로 int로 바꿔서 저장
	
	static int plantCnt, jumpCnt,ansX,ansY;
	
	static final int DIFF_PLUS = 0;
	static final int SUM_PLUS = 1;
	static final int SUM_MINUS = 2;
	static final int DIFF_MINUS = 3;
	
	static class Plant{
		int x,y,diff,sum;
		
		public Plant(int x, int y) {
			this.x = x;
			this.y = y;
			this.diff = x-y;
			this.sum = x+y;
		}
		
		public void remove() {
			sumMap.get(sum).remove(this);
			diffMap.get(diff).remove(this);
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
    	plantCnt = Integer.parseInt(st.nextToken());
    	jumpCnt = Integer.parseInt(st.nextToken());
    	ansX = -1;
    	ansY = -1;
    	
    	plants = new Plant[plantCnt];
    	jumpDir = new int[jumpCnt];
    	
    	String input = br.readLine();
    	for (int i = 0; i < jumpCnt; i++) {
    		jumpDir[i] = input.charAt(i) - 'A';
    	}
    	
    	for (int i = 0; i < plantCnt; i++) {
    		st = new StringTokenizer(br.readLine());
    		int x = Integer.parseInt(st.nextToken());
    		int y = Integer.parseInt(st.nextToken());
    		
    		plants[i] = new Plant(x,y);
    		
    		
    		
    	}

    	
    }
    
    public static void process() { 	
    	for (int i = 0; i < plantCnt; i++) {
    		Plant p = plants[i];
    		addToMap(p);
    	}
    	
    	Plant cur = plants[0];
    	
    	for (int i = 0; i< jumpCnt; i++) {
    		int dir = jumpDir[i];
    		
    		TreeSet<Plant> sumTree = sumMap.get(cur.sum);
    		TreeSet<Plant> diffTree = diffMap.get(cur.diff);
    		Plant temp = null;
    		
    		switch(dir) {
				case(SUM_PLUS):
					temp = sumTree.higher(cur);
					break;
				case(SUM_MINUS):
					temp = sumTree.lower(cur);
					break;
				case(DIFF_PLUS):
					temp = diffTree.higher(cur);
					break;
				case(DIFF_MINUS):
					temp = diffTree.lower(cur);
					break;
    		}
    		
    		if (temp == null) continue;

    		cur.remove();
    		cur = temp;
    		
    	}
    	
    	ansX = cur.x;
    	ansY = cur.y;
    	
    }


    private static void addToMap(Plant p) {
    	if (!sumMap.containsKey(p.sum)) {
    		sumMap.put(p.sum, new TreeSet<Plant>((p1,p2) -> p1.diff-p2.diff));
    	}
    	sumMap.get(p.sum).add(p);
    	
    	
    	if (!diffMap.containsKey(p.diff)) {
    		diffMap.put(p.diff, new TreeSet<Plant>((p1,p2) -> p1.sum-p2.sum));
    	} 
		diffMap.get(p.diff).add(p);
		
	}

	public static void print() {
    	System.out.println(ansX + " " + ansY);
    }
}
```
