```java
import java.util.*;
import java.io.*;

public class Main {
	
	// IO field
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
	static StringTokenizer st = new StringTokenizer("");

	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static String nextToken() throws Exception {
		while(!st.hasMoreTokens()) nextLine();
		return st.nextToken();
	}
	static int nextInt() throws Exception { return Integer.parseInt(nextToken()); }
	static long nextLong() throws Exception { return Long.parseLong(nextToken()); }
	static double nextDouble() throws Exception { return Double.parseDouble(nextToken()); }
	static void bwEnd() throws Exception {bw.flush();bw.close();}
	
	// Additional field
	
	static int N, K, D;
	static int[][] rules;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
		
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = nextInt();
		K = nextInt();
		D = nextInt();
		rules = new int[K][3];
		for(int i=0;i<K;i++) for(int j=0;j<3;j++) rules[i][j] = nextInt();
				
	}
	
	static void solve() throws Exception {
		
		int s = 1, e = N, m = (s+e)>>1;
		while(s<e) {
			long cnt = 0;
			for(int[] rule : rules) {
				int a = rule[0], b = rule[1], c = rule[2];
				if(m < a) continue;
				cnt += Math.min((m-a)/c + 1,  (b-a)/c + 1);
			}
			if(cnt < D) s = m+1;
			else e = m;
			m = (s+e)>>1;
		}
		bw.write(m + "\n");
		
	}
	
}
```
