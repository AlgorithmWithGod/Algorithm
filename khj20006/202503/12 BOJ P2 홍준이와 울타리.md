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
	
	static int N, X;
	static int[] A, B, C;
	
	public static void main(String[] args) throws Exception {
			
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		nextLine();
		N = nextInt();
		X = nextInt()-1;
		
		A = new int[N+1];
		
		nextLine();
		for(int i=1;i<=N;i++) A[i] = nextInt();

		
	}
	
	static void solve() throws Exception{
		
		fillB();
		fillC();
		
		
		long ans1 = 0;
		for(int i=1;i<=N;i++) ans1 += A[i] - C[i];
		
		long ans2 = 0;
		for(int i=1;i<=N;) {
			int a = C[i], cnt = 0;
			while(i<=N && C[i] == a) {
				i++;
				cnt++;
			}
			ans2 += (cnt - 1) / (X+1) + 1;
		}
		
		bw.write(ans1 + "\n" + ans2);
		
	}
	
	static void fillB() {
		
		Deque<int[]> D = new ArrayDeque<>();
		
		B = new int[N+1];
		for(int i=N;i>=1;i--) {
			while(!D.isEmpty() && D.peekLast()[0] >= A[i]) D.pollLast();
			D.offerLast(new int[] {A[i], i});
			while(!D.isEmpty() && D.peekFirst()[1] - i > X) D.pollFirst();
			if(B[i] <= N-X) B[i] = D.peekFirst()[0];
		}
		for(int i=N-X+1;i<=N;i++) B[i] = B[i-1];
		
	}
	
	static void fillC() {
		
		Deque<int[]> D = new ArrayDeque<>();
		
		C = new int[N+1];
		for(int i=1;i<=N;i++) {
			while(!D.isEmpty() && D.peekLast()[0] <= B[i]) D.pollLast();
			D.offerLast(new int[] {B[i], i});
			while(!D.isEmpty() && i - D.peekFirst()[1] > X) D.pollFirst();
			C[i] = D.peekFirst()[0];
		}
		
	}
	
}

```
