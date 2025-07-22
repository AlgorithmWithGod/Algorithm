```java
import java.util.*;
import java.io.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    
    public static void main(String[] args) throws Exception {
        int N = Integer.parseInt(br.readLine());
        int[] point = new int[N];
        int totalSum = 0;
        
        for (int i = 0; i < N; i++) {
            point[i] = Integer.parseInt(br.readLine());
            totalSum += point[i];
        }
        
        int left = 0;
        int right = 1;
        int clockwiseSum = point[0];
        int max = 0;
        
        while (left < N) {
            int counterClockwiseSum = totalSum - clockwiseSum;
            int distance = Math.min(clockwiseSum, counterClockwiseSum);
            max = Math.max(max, distance);
            
            if (clockwiseSum < counterClockwiseSum) {
                clockwiseSum += point[right];
                right = (right + 1) % N;
            } else {
                clockwiseSum -= point[left];
                left++;
            }
            
            if (left == right) break;
        }
        
        bw.write(Integer.toString(max));
        bw.close();
    }
}
```
