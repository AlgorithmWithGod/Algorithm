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
	static int gcd(int a, int b) {
		if(a < b) {
			int temp = a;
			a = b;
			b = temp;
		}
		return a%b==0 ? b : gcd(b,a%b);
	}
	
	public static void main(String[] args) throws Exception {

		nextLine();
		int a = nextInt();
		int b = nextInt();
		int c = nextInt();
		int d = nextInt();

		if((b-a)*(d-c) < 0) bw.write("NO");
		else if(b==a || c==d) bw.write(b-a == d-c ? "YES":"NO");
		else bw.write("YES");

		bwEnd();
	}

}

```
