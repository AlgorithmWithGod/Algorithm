```java

import java.util.*;

import java.io.*;
       
public class Solution {
           
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
     
    static long N, K;
     
    // 
       
    public static void main(String[] args) throws Exception {
          
        int TC = nextInt();
        for(int tc=1;tc<=TC;tc++) {
              
            ready();
            solve(tc);
              
        }
        bwEnd();
          
    }
       
    static void ready() throws Exception {
    	
    	N = nextInt();
    	K = nextInt();
    	
    }
    
    static void solve(int tc) throws Exception {
        bw.write("#" + tc + " ");
        
        long ans = 1;
        for(long i=2;i*i<=K;i++) {
        	long cnt = 0, d = 1;
        	while(K%i == 0) {
        		d *= i;
        		K /= i;
        		cnt++;
        	}
        	long ncnt = 0;
        	for(long j=i;j<=N;j*=i) ncnt += N/j;
        	while(cnt-ncnt>0) {
        		cnt--;
        		d /= i;
        	}
        	ans *= d;
        }
        if(N/K >= 1) ans *= K;
        bw.write(ans + "\n");
        
    }
     
}

```
