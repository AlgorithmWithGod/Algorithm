```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int n = Integer.parseInt(st.nextToken());
        int k = Integer.parseInt(st.nextToken());
        int[] arr = new int[n];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < n; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }
        int left = 0, right = 0;
        int odd = 0;
        int evenCount = 0;
        int answer = 0;
        while(right < n) {
            if (arr[right] % 2 == 0) {
                evenCount++;
            }else {
                odd++;
            }
            right++;

            while(odd > k){
                if(arr[left] % 2== 0) {
                    evenCount--;
                } else {
                    odd--;
                }
                left++;
            }
            answer = Math.max(answer, evenCount);
        }
        
        
        System.out.println(answer);
    }
}

```
