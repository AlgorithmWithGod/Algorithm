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
    static String str;
    static int[] left, right, R_cnt;
    static int N;
	
	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
        str = new String("0"); // padding for prefix sum
        str += br.readLine();
        str += "0";
        N = str.length()-2;

        left = new int[N+2];
        right = new int[N+2];
        R_cnt = new int[N+2];

	}
	
	static void solve() throws Exception{

        for(int i=1;i<=N;i++) left[i] += left[i-1] + (str.charAt(i) == 'K' ? 1 : 0);
        for(int i=N;i>=1;i--) right[i] += right[i+1] + (str.charAt(i) == 'K' ? 1 : 0);
        for(int i=1;i<=N;i++) R_cnt[i] += R_cnt[i-1] + (str.charAt(i) == 'R' ? 1 : 0);
        
        int ans = 0;
        int s = 0, e = N+1, K_cnt = 0;
        while(s<e){
            if(R_cnt[e-1] - R_cnt[s] == 0) break;
            ans = Math.max(ans, R_cnt[e-1] - R_cnt[s] + K_cnt*2);
            K_cnt++;
            while(s<=N && left[s] < K_cnt) s++;
            while(e>=1 && right[e] < K_cnt) e--;
        }
        bw.write(ans+"\n");
		
	}
	
}

```
