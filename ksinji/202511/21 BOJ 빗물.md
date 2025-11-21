```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int h = Integer.parseInt(st.nextToken());
        int w = Integer.parseInt(st.nextToken());

        int[] height = new int[w];

        st = new StringTokenizer(br.readLine());
        for (int i=0; i<w; i++){
            height[i] = Integer.parseInt(st.nextToken());
        }

        int answer=0, l=0;

        for (int i=1; i<w-1; i++){
            l = Math.max(l, height[i-1]);
            int r = 0;
            for (int j=i+1; j<w; j++){
                r = Math.max(r, height[j]);
            }

            if (height[i] < l && height[i] < r) answer+=Math.min(l, r)-height[i];
        }

        System.out.println(answer);
    }
}
```
