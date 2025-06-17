```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        
        int N = Integer.parseInt(br.readLine());
        
        int[] minDp = new int[3];
        int[] maxDp = new int[3];
        
        st = new StringTokenizer(br.readLine());
        for (int j = 0; j < 3; j++) {
            int value = Integer.parseInt(st.nextToken());
            minDp[j] = value;
            maxDp[j] = value;
        }
        
        for (int i = 1; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            int[] current = new int[3];
            for (int j = 0; j < 3; j++) {
                current[j] = Integer.parseInt(st.nextToken());
            }
            
            int[] tempMin = minDp.clone();
            int[] tempMax = maxDp.clone();
            
            minDp[0] = Math.min(tempMin[0], tempMin[1]) + current[0];
            minDp[1] = Math.min(tempMin[0], Math.min(tempMin[1], tempMin[2])) + current[1];
            minDp[2] = Math.min(tempMin[1], tempMin[2]) + current[2];
            
            maxDp[0] = Math.max(tempMax[0], tempMax[1]) + current[0];
            maxDp[1] = Math.max(tempMax[0], Math.max(tempMax[1], tempMax[2])) + current[1];
            maxDp[2] = Math.max(tempMax[1], tempMax[2]) + current[2];
        }
        
        int maxResult = Math.max(maxDp[0], Math.max(maxDp[1], maxDp[2]));
        int minResult = Math.min(minDp[0], Math.min(minDp[1], minDp[2]));
        
        System.out.println(maxResult + " " + minResult);
    }
}
```
