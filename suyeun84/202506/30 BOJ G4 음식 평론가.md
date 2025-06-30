```java
import java.io.*;
import java.util.*;

public class boj1188 {
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	
	public static void main(String[] args) throws Exception {
		nextLine();
		int N = nextInt();
		int M = nextInt();
		
		int div = M;
		while(div > 0) {
			int temp = N;
			N = div;
			div = temp % div;
		}
		System.out.println(M - N);
	}
}
```
