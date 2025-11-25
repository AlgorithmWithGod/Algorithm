```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main{
	private static int N;
	private static char[] Arr;
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		N = Integer.parseInt(br.readLine());
		Arr = new char[N];
		Deque<int[]> q = new ArrayDeque<>();
		Deque<int[]> buffer = new ArrayDeque<>();
		q.add(new int[]{0, N/2, 0});
		q.add(new int[]{N/2, N, 1});
		for(int i = 0; i<7; i++){
			while(!q.isEmpty()){
				int[] temp = q.poll();
				int s = temp[0]; int e = temp[1]; int isB = temp[2];
				putString(s, e, isB);

				if(s + 1 < e){
					buffer.add(new int[]{s, (s + e)/2, 0});
					buffer.add(new int[]{(s + e)/2, e, 1});
				}
			}
			while(!buffer.isEmpty()){
				q.add(buffer.poll());
			}
			System.out.println(String.valueOf(Arr));
		}
		// putString(0, N/2, false)+putString(N/2, N, true); // (0, N/2, false), (N/2, N, true)
		// putString(0, N/4, false) + putString(N/4, N/2, true)

		br.close();
	}

	private static void putString(int start, int end, int isB){
		for(int i = start; i<end; i++)
			Arr[i] = (isB==1) ? 'B':'A';
	}
}
```
