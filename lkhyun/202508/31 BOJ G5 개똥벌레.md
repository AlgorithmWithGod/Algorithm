```java
import java.io.*;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N,H;

    public static void main(String[] args) throws IOException {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        H = Integer.parseInt(st.nextToken());

        int[] top = new int[H+1];
        int[] bot = new int[H+1];
        for (int i = 0; i < N; i++) {
            int cur = Integer.parseInt(br.readLine());
            if(i%2 == 0){
                bot[cur]++;
            }else{
                top[cur]++;
            }
        }

        for (int i = H-1; i > 1; i--) {
            bot[i-1] += bot[i];
        }
        for (int i = H-1; i > 1; i--) {
            top[i-1] += top[i];
        }

        int min = N;
        int cnt = 0;
        for (int i = 1; i <= H; i++) {
            int cur = top[H-i+1] + bot[i];
            if(min == cur){
                cnt++;
            }else if(min > cur){
                min = cur;
                cnt = 1;
            }
        }

        bw.write(min+" "+cnt);
        bw.close();
    }
}
```
