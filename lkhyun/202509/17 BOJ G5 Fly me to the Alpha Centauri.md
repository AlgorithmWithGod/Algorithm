```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static StringBuilder sb = new StringBuilder();
    
    public static void main(String[] args) throws Exception {
        int T = Integer.parseInt(br.readLine());

        for (int i = 0; i < T; i++) {
            st = new StringTokenizer(br.readLine());
            int x = Integer.parseInt(st.nextToken());
            int y = Integer.parseInt(st.nextToken());
            int diff = (y-x);
            int cnt = 1;


            double candidate = Math.sqrt(diff);
            int temp = (int)candidate;
            if(candidate*candidate == temp*temp) {
                bw.write((temp*2 - 1)+"\n");
                continue;
            }else{
                cnt = temp;
            }
                        
            int rest = diff - cnt*cnt;
            if(rest>cnt) bw.write((cnt*2 + 1) + "\n");
            else bw.write((cnt*2)+"\n");
        }
        
        bw.close();
    }

}
```
