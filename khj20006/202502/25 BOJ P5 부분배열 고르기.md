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

    static int N;
    static int[] r;
    static long[] A, C;
    static int[][] L;
    static boolean[] V;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{

        N = Integer.parseInt(br.readLine());
        
        r = new int[N];
        C = new long[N];
        A = new long[N];
        L = new int[N][2];
        V = new boolean[N];
        nextLine();
        
        
        for(int i=0;i<N;i++) {
            r[i] = i;
            A[i] = nextLong();
            C[i] = A[i];
            L[i][0] = (int)A[i];
            L[i][1] = i;
        }
		
	}
	
	static void solve() throws Exception{
		
        Arrays.sort(L, (a,b) -> b[0]-a[0]);
        
        long ans = 0;
        for(int[] now : L){
            int v = now[0], i = now[1];
            if(i>0 && V[i-1]){
                int x = f(i), y = f(i-1);
                C[x] += C[y];
                r[y] = x;
            }
            if(i<N-1 && V[i+1]){
                int x = f(i), y = f(i+1);
                C[x] += C[y];
                r[y] = x;
            }
            V[i] = true;
            ans = Math.max(ans, v * C[f(i)]);
            
        }
        bw.write(ans + "\n");
		
	}
	
	static int f(int x) {
	    return x==r[x] ? x : (r[x]=f(r[x]));
	}
	
}

```
