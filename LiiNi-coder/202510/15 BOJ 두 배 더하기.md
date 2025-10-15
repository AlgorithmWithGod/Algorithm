```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int n = Integer.parseInt(br.readLine());
        StringTokenizer st = new StringTokenizer(br.readLine());
        int[] arr = new int[n];
        for(int i = 0; i < n; i++){
            arr[i] = Integer.parseInt(st.nextToken());
        }

        long answer = 0;
        while(true){
            for(int i = 0; i < n; i++){
                if(arr[i] % 2 == 1){
                    answer++;
                    arr[i] -= 1;
                }
            }
            if(Arrays.stream(arr).sum() == 0){
                break;
            }
            for(int i = 0; i<n; i++){
                arr[i] /= 2;
            }
            answer++;
        }
        System.out.println(answer);
        br.close();

    }
}

```
