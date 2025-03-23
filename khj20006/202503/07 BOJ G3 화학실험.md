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

	static int N, M;
	static int[] A, B;
	
	static PriorityQueue<int[]> Q = new PriorityQueue<>((a,b) -> {
		if(a[0] == b[0]) return a[1]-b[1];
		return a[0]-b[0];
	});
	static int[] cnt;
	
	public static void main(String[] args) throws Exception {
			
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
		N = Integer.parseInt(br.readLine());
		A = new int[N];
		B = new int[N];
		cnt = new int[1001001];
		for(int i=0;i<N;i++) {
			nextLine();
			A[i] = nextInt();
			B[i] = nextInt();
			Q.offer(new int[] {A[i]+B[i],A[i]});
			cnt[A[i]+B[i]]++;
		}
		
		M = Integer.parseInt(br.readLine()) - N;
		
	}
	
	static void solve() throws Exception{
		
		for(int i=0;i<M;i++) {
			int[] now = Q.poll();
			cnt[now[0]]--;
			cnt[now[0]+now[1]]++;
			Q.offer(new int[] {now[0]+now[1], now[1]});
		}
		int x = Q.poll()[0];
		if(cnt[x] == N) bw.write(x + "\n");
		else bw.write("0");
		
		
	}
	
}

```
