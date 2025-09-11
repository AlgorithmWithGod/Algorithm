```java
import java.io.*;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N;
    static int[] buildings;
    static int[] cnt;
    static int max;
    
    public static void main(String[] args) throws IOException {
        N = Integer.parseInt(br.readLine());
        buildings = new int[N+1];
        cnt = new int[N+1];

        st = new StringTokenizer(br.readLine());
        for (int i = 1; i <= N; i++) {
            buildings[i] = Integer.parseInt(st.nextToken());
        }

        for (int i = 1; i < N; i++) {
            for (int j = i+1; j <= N; j++) {
                double slope = (double)(buildings[j]-buildings[i]) / (j-i);
                boolean isPossible = true;
                for (int k = 1; i+k < j; k++) {
                    if(buildings[i]+(slope*k) <= buildings[i+k]){
                        isPossible = false;
                        break;
                    }
                }
                if(isPossible){
                    cnt[i]++;
                    cnt[j]++;
                }
            }
        }
        for (int i = 1; i <= N; i++) {
            max = Math.max(cnt[i], max);
        }
        bw.write(max+"");
        bw.close();
    }
}
```
