```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.awt.Point;
import java.util.ArrayDeque;
import java.util.Deque;
import java.util.EnumMap;
import java.util.HashSet;
import java.util.Iterator;
import java.util.Map;
import java.util.Set;

public class Main{
	private static int R, C;
	//private static int[][] Map;
	private static Set<Point> Enemies;
	private static Set<Point> tempEnemies;
	private static Set<Point> MustDestroy = new HashSet<>();
	private static Point Arduino;
	private static char[] IdsOfMoving = new char[100];
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		String[] tokens = br.readLine().split(" ");
		R = Integer.parseInt(tokens[0] );
		C = Integer.parseInt(tokens[1]);
		Enemies = new HashSet<>();
		tempEnemies = new HashSet<>();
		for(int r = 0; r<R; r++){

			char[] inputs = br.readLine().toCharArray();
			for(int c = 0; c<C; c++){
				char input = inputs[c];
				if(input == 'I'){
					Arduino = new Point(r, c);
				}else if(input == 'R'){
					Enemies.add(new Point(r, c));
				}
			}
		}
		IdsOfMoving = br.readLine().toCharArray();
		boolean isGameOver = false;
		int t;
		for(t = 0; t<IdsOfMoving.length; t++) {
			tempEnemies = new HashSet<>();
			char idOfMoving = IdsOfMoving[t];
			// 1. 입력에 따라 아두이노 이동
			// 입력에 따라 이동: O(1)
			int[] temp = getDrDc(idOfMoving);
			int dr = temp[0]; int dc = temp[1];
			Arduino.translate(dr, dc);

			// 2. 아두이노가 적칸에 있는지 확인 : O(1) <- 상태표시 Set에 판별
			if(Enemies.contains(Arduino)){
				// 맞다면 게임오버
				isGameOver = true;
				break;
			}
			// 3. 모든 적들을 순회하여 : 적들의 좌표를 바로 알수있도록 해야함 -> Set<Point>
			// 아두이노와 가까워지는 방향을 구한후 이동O(1): Set에서 삭제 후 이동후 삽입 -> 파괴해야할 것 Q에 넣음, 해당 칸에 아두이노 있는지확인
			Iterator<Point> iter = Enemies.iterator();
			while(iter.hasNext()){
				Point enemy = iter.next();
				temp = getDrDcForwardTo(enemy, Arduino);
				dr = temp[0]; dc = temp[1];
				Point np = new Point(enemy.x + dr, enemy.y + dc);
				boolean isNotOverlap = tempEnemies.add(np);
				if(!isNotOverlap){
					MustDestroy.add(np);
				}
			}
			Enemies = tempEnemies;
			// 4. 적들의 하나라도 아두이노 칸에 있다면 게임오버 :
			if(Enemies.contains(Arduino)){
				isGameOver = true;
				break;
			}
			// 5. 적이 겹쳐져 있는지를 파악 후 겹쳐져있다면 해당 적 모두 파괴 : 파괴Q를 poll하면서 파괴해나감
			iter = MustDestroy.iterator();
			while(iter.hasNext()){
				Point destroy = iter.next();
				Enemies.remove(destroy);
			}
			MustDestroy.clear();
			
		}

		if(isGameOver){
			System.out.print("kraj ");
			System.out.println(t+1);
		}else{
			print();
		}
		br.close();
	}

	private static void print() {
		String[] display = new String[R];
		for(int r = 0; r<R; r++){
			StringBuilder sb = new StringBuilder();
			for(int c = 0; c<C; c++)
				sb.append('.');
			display[r] = sb.toString();
		}
		int r, c;
		r = Arduino.x;
		c = Arduino.y;
		StringBuilder sb = new StringBuilder(display[r]);
		sb.setCharAt(c, 'I');
		display[r] = sb.toString();

		for(Point enemy: Enemies){
			r = enemy.x;
			c = enemy.y;
			sb = new StringBuilder(display[r]);
			sb.setCharAt(c, 'R');
			display[r] = sb.toString();
		}
		for(r = 0; r<R; r++){
			System.out.println(display[r]);
		}
	}

	private static int[] getDrDcForwardTo(Point me, Point target) {
		int dr, dc;
		if(me.x < target.x){
			dr = 1;
		}else if(me.x > target.x){
			dr = -1;
		}else{
			dr = 0;
		}
		if(me.y < target.y){
			dc = 1;
		}else if(me.y > target.y){
			dc = -1;
		}else{
			dc = 0;
		}
		return new int[]{dr,dc};
	}

	private static int[] getDrDc(char idOfMoving) {
		int[][] drdcs = new int[][]{
			{}, //0
			{1, -1},
			{1, 0},
			{1, 1},
			{0, -1},
			{0, 0},
			{0, 1},
			{-1, -1},
			{-1, 0},
			{-1, 1}
		};
		return drdcs[idOfMoving - '0'];
	}
}
```
