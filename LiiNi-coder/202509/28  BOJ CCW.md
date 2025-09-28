```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        
        st = new StringTokenizer(br.readLine());
        long x1 = Long.parseLong(st.nextToken());
        long y1 = Long.parseLong(st.nextToken());
        
        st = new StringTokenizer(br.readLine());
        long x2 = Long.parseLong(st.nextToken());
        long y2 = Long.parseLong(st.nextToken());
        
        st = new StringTokenizer(br.readLine());
        long x3 = Long.parseLong(st.nextToken());
        long y3 = Long.parseLong(st.nextToken());

        long value = (x2 - x1) * (y3 - y1) - (x3 - x1) * (y2 - y1); // 외적
        if(value > 0) {
            System.out.println(1);
        }else if(value < 0) {
            System.out.println(-1);
        }else{
            System.out.println(0);
        }
    }
}
```
