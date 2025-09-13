```java
import java.io.*;
import java.util.*;

public class Main {
    
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N;
    static int[] arr;

    public static void main(String[] args) throws IOException {
        N = Integer.parseInt(br.readLine());
        arr = new int[N];

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }
        int left = 0;
        int right = N-1;
        int ans = 0;
        while(left < right){           
            if(arr[left] <= arr[right]){
                ans = Math.max(ans,(right-left-1)*arr[left]);
                left++;
            }else{
                ans = Math.max(ans,(right-left-1)*arr[right]);
                right--;
            }
        }
        bw.write(ans+"");
        bw.close();
    }
}
```
