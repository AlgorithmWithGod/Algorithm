```java
import java.io.*;
import java.util.*;

public class boj1091 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
    static int nextInt() {return Integer.parseInt(st.nextToken());}

    static int N;
    static int[] P, S, cur, start;
    public static void main(String[] args) throws Exception {
    	  int answer = 0;
        nextLine();
        N = nextInt();
        nextLine();
        P = new int[N];
        cur = new int[N];
        start = new int[N];
        for (int i = 0; i < N; i++) {
        	P[i] = nextInt();
        	cur[i] = i;
        }
        start = cur.clone();
        nextLine();
        S = new int[N];
        for (int i = 0; i < N; i++) S[i] = nextInt();
        
        if (check()) {
            System.out.println(0);
            return;
        }
        
        while (true) {
        	int[] temp = new int[N];
        	for (int i = 0; i < N; i++) temp[S[i]] = cur[i];
        	answer++;
        	cur = temp;
        	if (check()) break;
        	if (Arrays.equals(cur, start)) {
        		answer = -1;
        		break;
        	}
        }
        System.out.println(answer);
    }
    
    static boolean check() {
    	int[] pos = new int[N];
        for (int i = 0; i < N; i++) pos[cur[i]] = i;
    	for (int i = 0; i < N; i++) {
    		if (pos[i] % 3 != P[i]) return false;
    	}
    	return true;
    }
}
```
