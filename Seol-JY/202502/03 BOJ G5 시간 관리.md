```java
import java.util.*;
import java.io.*;

public class Main {    
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        Pair[] pairs = new Pair[N];
        
        for (int i = 0; i < N; i++) {
        	StringTokenizer st = new StringTokenizer(br.readLine());
        	int t = Integer.parseInt(st.nextToken());
        	int s = Integer.parseInt(st.nextToken());
        	pairs[i] = new Pair(t, s);
        }
        
        Arrays.sort(pairs, (x, y) -> x.s - y.s);
        
        
        int nowTime = 0;
        Integer ans = null;
        for (Pair p : pairs) {
        	nowTime += p.t;
        	
        	if (nowTime > p.s) {
        		System.out.println(-1);
        		return;
        	}
        	
        	if (ans == null) {
        		ans = p.s - nowTime;
        	} else {
            	ans = Math.min (ans, p.s - nowTime);
        	}
        }
        
		System.out.println(ans);
    }
    
    static class Pair {
    	int t;
    	int s;
    	
    	public Pair(int t, int s) {
    		this.t = t;
    		this.s = s;
    	}
    }
}

```
