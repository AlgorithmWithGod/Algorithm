```java

import java.util.*;
import java.io.*;

class Main {
	
	// IO field
	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
	static StringTokenizer st = new StringTokenizer("");

	static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
	static int nextInt() throws Exception {
		if(!st.hasMoreTokens()) nextLine();
		return Integer.parseInt(st.nextToken());
	}
	static long nextLong() throws Exception {
		if(!st.hasMoreTokens()) nextLine();
		return Long.parseLong(st.nextToken());
	}
	static void bwEnd() throws Exception {bw.flush();bw.close();}
	
	// Additional field
	
	static int a, b;
	
	public static void main(String[] args) throws Exception {
		
		for(int T=nextInt();T-->0;) {
			
			ready();
			solve();
		}
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		a = nextInt();
		b = nextInt();
		
		
	}
	
	static void solve() throws Exception{
		
		
		char g = 'A';
		if(a<b) {
			int t = a;
			a = b;
			b = t;
			g = 'B';
		}
		if((a+b)%2 == 1) bw.write("-1\n");
		else {
			int half = (a-b)/2;
			if(half > 0 && (half&a) == half) bw.write("1\n" + g + " " + half + "\n");
			else bw.write("2\n" + g + " " + half + "\n" + g + " " + half + "\n");			
		}
		
	}
	
}

```
