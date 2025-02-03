```java

import java.util.*;
import java.io.*;

class Main {
	
	// IO field
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
	static StringTokenizer st;

	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() {return Integer.parseInt(st.nextToken());}
	static long nextLong() {return Long.parseLong(st.nextToken());}
	static void bwEnd() throws Exception {bw.flush();bw.close();}
	
	// Additional field
	

	public static void main(String[] args) throws Exception {

		nextLine();
		int N = nextInt();
		int[] A = new int[N];
		for(int i=0;i<N;i++) A[i] = Integer.parseInt(br.readLine());
		Arrays.sort(A);
		
		long ans = 0;
		int c = 1;
		for(int i=0;i<N;i++) {
			int p = i;
			while(i<N-1 && A[i] == A[i+1] && A[i] == c) i++;
			ans += (long)(i-p+1)*Math.max(0,A[p]-c++);
		}
		bw.write(ans+"\n");
		
		
		bwEnd();
	}

}

```
