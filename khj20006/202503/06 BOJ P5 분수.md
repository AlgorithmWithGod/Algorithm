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

	static long T, I, N;
	static String A, B;
	
	public static void main(String[] args) throws Exception {
		
		T = Integer.parseInt(br.readLine());
		while(T-- > 0) {
			
			ready();
			solve();
			
		}
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		nextLine();
		A = st.nextToken();
		B = st.nextToken();
		
		nextLine();
		I = nextLong();
		N = nextLong();
		
	}
	
	static void solve() throws Exception{
		
		BigInteger a = new BigInteger(A);
		BigInteger b = new BigInteger(B);
		a = a.mod(b);
		
		// a가 더 작으면
		BigInteger t = power(new BigInteger("10"), I-1, b);
		a = a.multiply(t).mod(b);
		for(int i=0;i<N;i++) {
			bw.write(a.multiply(new BigInteger("10")).divide(b).toString().charAt(0));
			a = a.multiply(new BigInteger("10")).mod(b);
		}
		bw.write("\n");
		
	}
	
	static BigInteger power(BigInteger x, long p, BigInteger m) {
		if(p == 0) return new BigInteger("1");
		if(p == 1) return x.mod(m);
		BigInteger half = power(x, p>>1, m).mod(m);
		half = half.multiply(half).mod(m);
		if(p%2 == 0) return half;
		return half.multiply(x).mod(m);
	}
	
}

```
