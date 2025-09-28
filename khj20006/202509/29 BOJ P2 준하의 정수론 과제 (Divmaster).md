```java
import java.io.*;
import java.util.*;

class IOController {
	BufferedReader br;
	BufferedWriter bw;
	StringTokenizer st;

	public IOController() {
		br = new BufferedReader(new InputStreamReader(System.in));
		bw = new BufferedWriter(new OutputStreamWriter(System.out));
		st = new StringTokenizer("");
	}

	String nextLine() throws Exception {
		String line = br.readLine();
		st = new StringTokenizer(line);
		return line;
	}

	String nextToken() throws Exception {
		while (!st.hasMoreTokens())
			nextLine();
		return st.nextToken();
	}

	int nextInt() throws Exception {
		return Integer.parseInt(nextToken());
	}

	long nextLong() throws Exception {
		return Long.parseLong(nextToken());
	}

	double nextDouble() throws Exception {
		return Double.parseDouble(nextToken());
	}

	void close() throws Exception {
		bw.flush();
		bw.close();
	}

	void write(String content) throws Exception {
		bw.write(content);
	}

}

public class Main {

	static IOController io;

	//

	static int N, Q;
	static int[] f, g, sieve, max;
	static long[] sum;

	public static void main(String[] args) throws Exception {

		io = new IOController();

		preprocess(1_000_000);

		N = io.nextInt();
		Q = io.nextInt();
		max = new int[N*4];
		sum = new long[N*4];
		for(int i=1;i<=N;i++) {
			int a = io.nextInt();
			pointUpdate1(1,N,i,a,1);
			pointUpdate2(1,N,i,g[a],1);
		}

		while(Q-->0) {
			int o = io.nextInt();
			int s = io.nextInt();
			int e = io.nextInt();
			if(o == 1) rangeUpdate(1,N,s,e,1);
			else io.write(find(1,N,s,e,1) + "\n");
		}

		io.close();

	}

	private static void preprocess(int limit) {
		sieve = new int[limit+1];
		for(int i=2;i*i<=limit;i++) if(sieve[i] == 0) for(int j=i*i;j<=limit;j+=i) if(sieve[j] == 0) sieve[j] = i;

		f = new int[limit+1];
		g = new int[limit+1];
		f[1] = 1;
		f[2] = 2;
		for(int i=3;i<=limit;i++) {
			int t = i, prev = 0, cnt = 0;
			f[i] = 1;
			while(sieve[t] != 0) {
				if(prev != sieve[t]) {
					f[i] *= (cnt+1);
					cnt = 0;
					prev = sieve[t];
				}
				cnt++;
				t /= sieve[t];
			}
			if(t == 1) f[i] *= (cnt+1);
			else {
				if(prev == t) f[i] *= (cnt+2);
				else f[i] *= (cnt+1) * 2;
			}
			g[i] = g[f[i]] + 1;
		}
	}

	private static void pointUpdate1(int s, int e, int i, int v, int n) {
		if(s == e) {
			sum[n] = v;
			return;
		}
		int m = (s+e)>>1;
		if(i <= m) pointUpdate1(s,m,i,v,n*2);
		else pointUpdate1(m+1,e,i,v,n*2+1);
		sum[n] = sum[n*2] + sum[n*2+1];
	}

	private static void pointUpdate2(int s, int e, int i, int v, int n) {
		if(s == e) {
			max[n] = v;
			return;
		}
		int m = (s+e)>>1;
		if(i <= m) pointUpdate2(s,m,i,v,n*2);
		else pointUpdate2(m+1,e,i,v,n*2+1);
		max[n] = Math.max(max[n*2], max[n*2+1]);
	}

	private static void rangeUpdate(int s, int e, int l, int r, int n) {
		if(l>r || l>e || r<s) return;
		if(max[n] == 0) return;
		if(s == e) {
			sum[n] = f[(int)sum[n]];
			max[n] = g[(int)sum[n]];
			return;
		}
		int m = (s+e)>>1;
		if(max[n*2] > 0) rangeUpdate(s,m,l,r,n*2);
		if(max[n*2+1] > 0) rangeUpdate(m+1,e,l,r,n*2+1);
		sum[n] = sum[n*2] + sum[n*2+1];
		max[n] = Math.max(max[n*2], max[n*2+1]);
	}

	private static long find(int s, int e, int l, int r, int n) {
		if(l>r || l>e || r<s) return 0;
		if(l<=s && e<=r) return sum[n];
		int m = (s+e)>>1;
		return find(s,m,l,r,n*2) + find(m+1,e,l,r,n*2+1);
	}

}
```
