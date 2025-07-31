```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        
        int t = Integer.parseInt(br.readLine());
        
        for (int tc = 0; tc < t; tc++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int n = Integer.parseInt(st.nextToken());
            int k = Integer.parseInt(st.nextToken());
            
            int[] arr = new int[n];
            st = new StringTokenizer(br.readLine());
            for (int i = 0; i < n; i++) {
                arr[i] = Integer.parseInt(st.nextToken());
            }
            
            Arrays.sort(arr);
            
            int left = 0;
            int right = n - 1;
            int minDiff = Integer.MAX_VALUE;
            int count = 0;
            
            while (left < right) {
                int sum = arr[left] + arr[right];
                int diff = Math.abs(sum - k);
                
                if (diff < minDiff) {
                    minDiff = diff;
                    count = 1;
                } else if (diff == minDiff) {
                    count++;
                }
                
                if (sum < k) {
                    left++;
                } else {
                    right--;
                }
            }
            
            sb.append(count).append('\n');
        }
        
        System.out.print(sb);
    }
}
```
