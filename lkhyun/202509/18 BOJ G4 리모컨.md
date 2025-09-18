```java
import java.io.*;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N, M;
    static boolean[] broken = new boolean[10];
    
    public static void main(String[] args) throws IOException {
        N = Integer.parseInt(br.readLine());
        M = Integer.parseInt(br.readLine());
        if(M!=0){
            st = new StringTokenizer(br.readLine());
        for (int i = 0; i < M; i++) {
            broken[Integer.parseInt(st.nextToken())] = true;
        }
        }
        
        int result = Math.abs(N - 100);
        
        for (int channel = 0; channel <= 1000000; channel++) {
            int cnt = getCount(channel);
            if (cnt > 0) {
                int total = cnt + Math.abs(N - channel);
                result = Math.min(result, total);
            }
        }
        
        bw.write(result+"");
        bw.close();
    }
    
    static int getCount(int channel) {
        if (channel == 0) {
            return broken[0] ? -1 : 1;
        }
        
        int count = 0;
        int temp = channel;
        
        while (temp > 0) {
            int digit = temp % 10;
            if (broken[digit]) {
                return -1;
            }
            count++;
            temp /= 10;
        }
        
        return count;
    }
}
```
