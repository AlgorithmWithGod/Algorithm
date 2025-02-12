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
	static List<int[]> arr;
	static boolean[] del;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
	}
	
	static void ready() throws Exception{

		N = Integer.parseInt(br.readLine());
		M = Integer.parseInt(br.readLine());
		arr = new ArrayList<>();
		del = new boolean[M+1];
		for(int i=1;i<=M;i++) {
			nextLine();
			int a = nextInt(), b = nextInt();
			if(a < b) {
				arr.add(new int[] {a,b,i});
				arr.add(new int[] {N+a,N+b,i});
			}
			else {
				arr.add(new int[] {a,N+b,i});
			}
		}
		
	}
	
	static void solve() throws Exception{
		
		Collections.sort(arr, (a,b) -> {
			if(a[0] == b[0]) return b[1]-a[1];
			return a[0]-b[0];
		});
		
		int mx = 0;
		for(int[] now : arr) {
			int l = now[0], r = now[1], x = now[2];
			if(r<=mx) del[x] = true;
			else mx = r;
		}
		for(int i=1;i<=M;i++) if(!del[i]) bw.write(i + " ");
		
		
	}
	
}

```
