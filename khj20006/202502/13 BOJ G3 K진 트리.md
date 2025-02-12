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
	static long N, K, Q;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
	}
	
	static void ready() throws Exception{

		nextLine();
		N = nextLong();
		K = nextLong();
		Q = nextLong();

	}
	
	static void solve() throws Exception{

		while(Q-- > 0) {
			nextLine();
			long x = nextLong(), y = nextLong();
			bw.write(dist(x-1,y-1) + "\n");
		}
		
	}
	
	static long dist(long x, long y) throws Exception{
		if(K == 1) return Math.abs(x-y);
		List<Long> X = find(x), Y = find(y);
		int i = X.size()-1, j = Y.size()-1;
		
		while(i>=0 && j>=0 && X.get(i).equals(Y.get(j))){
			i--;
			j--;
		}
		return i+j+2;
	}
	
	static List<Long> find(long x){
		List<Long> result = new ArrayList<>();
		
		result.add(x);
		while(x > 0) {
			x = (x-1)/K;
			result.add(x);
		}
		return result;
	}
	
}

```
