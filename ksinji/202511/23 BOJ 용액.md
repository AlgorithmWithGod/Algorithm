```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        StringTokenizer st = new StringTokenizer(br.readLine());
        
        int[] value = new int[n];

        for (int i=0; i<n; i++){
            value[i] = Integer.parseInt(st.nextToken());
        }

        int l = 0, r = n-1;
        int bestL = 0, bestR = n-1;
        int bestSum = value[l]+value[r];
        
        while(l < r){
            int sum = value[l] + value[r];

            if (Math.abs(sum) < Math.abs(bestSum)){
                bestSum = sum;
                bestL = l;
                bestR = r;
            }

            if (sum > 0) r--;
            if (sum < 0) l++;
            if (sum == 0) break;
        }

        System.out.println(value[bestL] + " " + value[bestR]);
    }
}
```
