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

	static int N;
	static int ans = 0;
	static int[] A = new int[8];
	
	static void sol(int pos, int choose, int[] arr) {
		if(pos == N) {
			int res = 0;
			for(int i=1;i<N;i++) {
				if(arr[i] < 50) continue;
				for(int j=0;j<i;j++){
					if(arr[j] == arr[i]-50) {
						res++;
						break;
					}
				}
			}
			ans = Math.max(ans, res);
			return;
		}
		for(int i=0;i<N;i++) {
			if((choose & (1<<i)) != 0) continue;
			arr[pos+1] = arr[pos] + A[i];
			sol(pos+1, choose | (1<<i), arr);
			arr[pos+1] = 0;
		}
	}

	public static void main(String[] args) throws Exception {

		N = Integer.parseInt(br.readLine());
		nextLine();
		for(int i=0;i<N;i++) A[i] = nextInt();
		sol(0, 0, new int[N+1]);
		
		bw.write(ans+"\n");
		
		bwEnd();
	}

}

```
