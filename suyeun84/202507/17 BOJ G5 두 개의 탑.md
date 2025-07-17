```java
import java.util.*;
import java.io.*;

public class boj2118 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
    static int nextInt() {return Integer.parseInt(st.nextToken());}

    public static void main(String[] args) throws Exception {
        nextLine();
        int N = nextInt();
        int sum = 0;
        int[] dist = new int[N+1];

        for(int i=0;i<N;i++){
            nextLine();
            dist[i] = nextInt();
            sum += dist[i];
        }

        int start = 0, last = 0, result = 0;
        int now = dist[start];

        while(start <= last && last < N){
            int minNow = Integer.min(now,sum - now);
            result = Integer.max(result, minNow);
            if(now == minNow){
                last++;
                now += dist[last];
            }
            else{
                now -= dist[start];
                start++;
            }
        }
        System.out.println(result);
    }
}
```
