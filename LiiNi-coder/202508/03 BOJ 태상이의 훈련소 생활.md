```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.Iterator;
import java.util.StringTokenizer;

public class Main {
	private static int M;
	private static int N;
	private static BufferedReader br;
	private static int[] A;
	private static int[] diffArr;

	public static void main(String[] args) throws IOException {
		br = new BufferedReader(new InputStreamReader(System.in));
		String[] temp = br.readLine().split(" ");
		N = Integer.parseInt(temp[0]);
		M = Integer.parseInt(temp[1]);
		diffArr = new int[N+1]; // 차분배
		A = new int[N];
		StringTokenizer st = new StringTokenizer(br.readLine());
		for(int i = 0; i<N; i++)
			A[i] = Integer.parseInt(st.nextToken());
		for(int m = 0; m<M; m++) {
			st = new StringTokenizer(br.readLine());
			int a = Integer.parseInt(st.nextToken())-1;
			int b = Integer.parseInt(st.nextToken()) ;
			int diff = Integer.parseInt(st.nextToken());
			diffArr[a] += diff;
			diffArr[b] += -diff;
		}
		for(int i = 1; i<N; i++) {
			diffArr[i] += diffArr[i-1];
		}
		//System.out.println(Arrays.toString(diffArr));
		StringBuilder sb = new StringBuilder();
		for(int i = 0; i<N;i++) {
			A[i] += diffArr[i];
			sb.append(A[i]);
			sb.append(" ");
		}
		System.out.println(sb.toString());
		br.close();
	}

}
```
