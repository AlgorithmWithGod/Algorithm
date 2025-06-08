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
		while(!st.hasMoreTokens()) nextLine();
		return st.nextToken();
	}
	static int nextInt() throws Exception { return Integer.parseInt(nextToken()); }
	static long nextLong() throws Exception { return Long.parseLong(nextToken()); }
	static double nextDouble() throws Exception { return Double.parseDouble(nextToken()); }
	static void bwEnd() throws Exception {bw.flush();bw.close();}
	
	// Additional field
	
	static int N;
	static int[] A, max;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = nextInt();
		A = new int[N+1];
		for(int i=1;i<=N;i++) A[i] = nextInt();
		max = new int[N+1];

	}
	
	static void solve() throws Exception{
		
		for(int i=1;i<=N;i++) max[i] = Math.max(max[i-1], A[i]);
		
		int min = -1;
		Stack<Integer> ans = new Stack<>();
		ans.add(N+1);
		for(int i=N;i>=1;) {
			int j = i, tempMin = A[i];
			while(j>=1 && max[j] == max[i]) {
				tempMin = Math.min(tempMin, A[j]);
				j--;
			}
			if(min == -1) min = tempMin;
			else {				
				if(max[i] <= min) ans.add(i+1);
				min = Math.min(min, tempMin);
			}
			i = j;
		}
		if(!ans.isEmpty() && ans.peek() != 1) ans.add(1);
		
		bw.write((ans.size()-1) + "\n");
		int now = ans.pop();
		while(!ans.isEmpty()) {
			int next = ans.pop();
			bw.write((next-now) + " ");
			for(int i=now;i<next;i++) bw.write(i + " ");
			bw.write("\n");
			now = next;
		}
		
	}
	
}

```
