```java
import java.util.*;
import java.io.*;

class Solution
{
	static int N;
	static int[] len;
	static int answer = Integer.MAX_VALUE;
    public static void main(String[] args) throws Exception{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

	    N = Integer.parseInt(st.nextToken());
	    len = new int[N];
	    st = new StringTokenizer(br.readLine());
	    for (int i = 0; i < N; i++) {
	    	len[i] = Integer.parseInt(st.nextToken());
	    }
	    
	    Arrays.sort(len);
	    
	    for (int i = 0; i < N; i++) {
	    	for (int j = i+1; j < N; j++) {
	    		calc(i, j);
	    		if (answer == 0) {
	    			System.out.println(0);
	    			return;
	    		}
	    	}
	    }
	    if (answer == Integer.MAX_VALUE) System.out.println(0);
	    else System.out.println(answer);
    }
    
    static void calc(int s1, int e1) {
    	int res = len[s1] + len[e1];
    	int start = 0;
    	int end = N-1;
    	while (start < end) {
    		int cal = len[start] + len[end];
    		if (s1 != start && e1 != end && s1 != end && e1 != start) {
    			answer = Math.min(answer, Math.abs(res-cal));
    		}
    		if (res >= cal) {
    			start += 1;
    		} else {
    			end -= 1;
    		}
    	}
    }
}

```
