```java
import java.io.*;
import java.util.*;
public class Main {
	private static BufferedReader br;
	private static int H, W;
	private static int[] Walls;
	private static StringTokenizer st;
	public static void main(String[] args) throws IOException {
		br = new BufferedReader(new InputStreamReader(System.in));
		String[] temp = br.readLine().split(" ");
		H = Integer.parseInt(temp[0]);
		W = Integer.parseInt(temp[1]);
		
		st = new StringTokenizer(br.readLine());
		int answer = 0;
		int sum = 0;

		int leftH = Integer.parseInt(st.nextToken());
		for(int w = 1; w<W; w++) {
			int wall = Integer.parseInt(st.nextToken());
			if(wall < leftH) {
				sum += leftH - wall;
				continue;
			}
			leftH = wall;
			answer += sum;
			sum = 0;
		}
		answer -= sum;
		System.out.println(answer);
		br.close();
		
	}
}
```
