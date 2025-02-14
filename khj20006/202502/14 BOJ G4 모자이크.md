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
    static int N, M, C, K;
	static List<int[]> wrong;
    static boolean[] exist;
    static int max_x = 0;

	public static void main(String[] args) throws Exception {
		
		ready();
		solve();
	
		bwEnd();
		
	}
	
	static void ready() throws Exception{
		
        nextLine();
        N = nextInt();
        M = nextInt();

        C = Integer.parseInt(br.readLine());
        K = Integer.parseInt(br.readLine());
        wrong = new ArrayList<>();
        exist = new boolean[M+1];

        for(int i=0;i<K;i++){
            nextLine();
            int x = nextInt(), y = nextInt();
            wrong.add(new int[]{x,y});
            max_x = Math.max(max_x, x);
            exist[y] = true;
        }

	}
	
	static void solve() throws Exception{

        int s = max_x, e = M, m = (s+e) >> 1;
        while(s < e){

            // m 센티미터의 색종이들 C개로 다 가릴 수 있는지?
            int cnt = 0;
            int p = 1;
            while(p <= M){
                while(p <= M && !exist[p]) p++;
                if(p > M) break;
                cnt++;
                p += m;
            }

            if(cnt > C) s = m+1;
            else e = m;
            m = (s+e)>>1;

        }

        bw.write(m+"\n");

	}
	
}

```
