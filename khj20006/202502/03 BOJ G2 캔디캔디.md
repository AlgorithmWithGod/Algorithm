```java

import java.util.*;
import java.io.*;
import java.math.BigInteger;

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
		long M = nextInt();
		int N = nextInt();
		Integer[] A = new Integer[N];
		for(int i=0;i<N;i++) A[i] = Integer.parseInt(br.readLine());
		Arrays.sort(A, Comparator.reverseOrder());
		
		for(int i=1;i<N;i++) {
			long cnt = i, diff = A[i-1] - A[i];
			
			if(M >= cnt * diff) {
				M -= cnt*diff;
			}
			else {
				for(int j=0;j<M%cnt;j++) A[j] = A[i-1] - (int)(M/cnt + 1);
				for(int j=(int)(M%cnt);j<i;j++) A[j] = A[i-1] - (int)(M/cnt);
				M = 0;
				break;
			}
		}
		
		if(M != 0) {
			for(int j=0;j<M%N;j++) A[j] = A[N-1] - (int)(M/N + 1);
			for(int j=(int)(M%N);j<N;j++) A[j] = A[N-1] - (int)(M/N);
		}

		BigInteger ans = new BigInteger("0");
		for(int i=0;i<N;i++) {
			BigInteger temp = new BigInteger(A[i].toString());
			ans = ans.add(temp.multiply(temp));
		}
		bw.write(ans.mod(new BigInteger("18446744073709551616"))+" ");
		
		bwEnd();
	}

}

```
