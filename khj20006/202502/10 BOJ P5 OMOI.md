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
	static int[] C;
	static List<Integer>[] V;
	static int N;
	static int[] cnt, mn;
	static long[] sum;
	static long ans = 0;
	
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
	}
	
	static void ready() throws Exception{

		N = Integer.parseInt(br.readLine());
		V = new List[N+1];
		for(int i=1;i<=N;i++) V[i] = new ArrayList<>();
		C = new int[N+1];
		cnt = new int[N+1];
		mn = new int[N+1];
		sum = new long[N+1];
		
		nextLine();
		for(int i=2;i<=N;i++) V[nextInt()].add(i);
		nextLine();
		for(int i=2;i<=N;i++) C[i] = nextInt();
		
	}
	
	static void solve() throws Exception{

		dfs(1);
		bw.write(ans+"\n");
		
	}
	
	static void dfs(int n) {
		mn[n] = Integer.MAX_VALUE;
		cnt[n] = 1;
		sum[n] = C[n];
		int mxCnt = 0;
		for(int i:V[n]) {
			dfs(i);
			cnt[n] += cnt[i];
			sum[n] += sum[i];
			mxCnt = Math.max(mxCnt, cnt[i]);
			mn[n] = Math.min(mn[n], mn[i]);
		}
		ans += sum[n] - C[n];
		if(mxCnt > cnt[n]-1-mxCnt) {
			long rem = cnt[n]-1 - (cnt[n]-1-mxCnt)*2;
			int minValue = Integer.MAX_VALUE;
			for(int i:V[n]) {
				if(cnt[i] == mxCnt) continue;
				minValue = Math.min(minValue, mn[i]);
			}
			ans += rem * minValue;
		}
		else {
			if((cnt[n]-1) % 2 != 0) {
				ans += mn[n];
			}
		}
		mn[n] = Math.min(mn[n], C[n]);
	}
	
}

```
