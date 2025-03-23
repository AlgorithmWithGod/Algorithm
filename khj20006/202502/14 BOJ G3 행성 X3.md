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
	static long ans = 0;
	static long[] cnt;
	static long N;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{

		cnt = new long[20];
		N = Integer.parseInt(br.readLine());
		for(int i=0;i<N;i++) {
			int a = Integer.parseInt(br.readLine());
			for(int j=0;j<20;j++) if((a & (1<<j)) != 0) cnt[j]++;
		}
		
	}
	
	static void solve() throws Exception{
		
		for(int i=0;i<20;i++) {
			ans += (N-cnt[i]) * cnt[i] * (1<<i);
		}
		bw.write(ans+"\n");
		
	}
	
}

```
