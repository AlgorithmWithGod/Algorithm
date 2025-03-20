```java

import java.util.*;
import java.io.*;

class Main {
	
	// IO field
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
	static StringTokenizer st = new StringTokenizer("");

	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static String nextToken() throws Exception {
		if(!st.hasMoreTokens()) nextLine();
		return st.nextToken();
	}
	static int nextInt() throws Exception { return Integer.parseInt(nextToken()); }
	static long nextLong() throws Exception { return Long.parseLong(nextToken()); }
	static double nextDouble() throws Exception { return Double.parseDouble(nextToken()); }
	static void bwEnd() throws Exception {bw.flush();bw.close();}
	
	// Additional field
	
	static int N, M, K;
	static long[] p;
	static long ans;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = nextInt();
		M = nextInt();
		K = nextInt()+1;
		p = new long[N];
		for(int i=0;i<N;i++) p[i] = nextInt();
		
	}
	
	static void solve() throws Exception{

		ans = M;
		bck(M,0,0,0);
		bw.write(ans + "\n");

	}
	
	static void bck(long curMoney, long borrow, long count, int day) {
		if(day == N) {
			ans = Math.max(ans, curMoney);
			return;
		}
		if(count > 0) {
			bck(curMoney, borrow, count, day+1);
			long benefit = count * p[day];
			curMoney += benefit;
			ans = Math.max(ans, curMoney);
			curMoney -= borrow;
			if(curMoney < 0) return;
			borrow = 0;
			count = 0;
		}
		bck(curMoney, borrow, count, day+1);
		borrow = curMoney * (K-1);
		curMoney *= K;
		count = curMoney / p[day];
		curMoney -= count * p[day];
		if(count > 0) bck(curMoney, borrow, count, day+1);
		
	}
	
}

```
