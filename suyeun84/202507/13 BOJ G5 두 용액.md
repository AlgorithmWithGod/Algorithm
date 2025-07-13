```java
import java.util.*;
import java.io.*;

public class boj2470 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	
	public static void main(String[] args) throws Exception {
		nextLine();
		int N = nextInt();
		int[] num = new int[N];
		nextLine();
		for (int i = 0; i < N; i++) num[i] = nextInt();
		Arrays.sort(num);
		
		int check = Integer.MAX_VALUE;
		int answer1 = 0, answer2 = 0;
		int low = 0, high = N-1;
			
		while(low<high) {
			int sum = num[low]+num[high];
				
			if(Math.abs(sum)<check) {
				check = Math.abs(sum);
				answer1 = num[low];
				answer2 = num[high];
			}	
			if(sum < 0) low++;
			else high--;		
		}
		System.out.println(answer1+" "+answer2);
	}
}
```
