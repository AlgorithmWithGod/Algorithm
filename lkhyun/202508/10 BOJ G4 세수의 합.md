```java
import java.util.*;
import java.io.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static int N;
    static int[] arr;

    public static void main(String[] args) throws Exception {
        N = Integer.parseInt(br.readLine());
        arr = new int[N];

        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(br.readLine());
        }
        Arrays.sort(arr);
        
        Set<Integer> sums = new HashSet<>();
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                sums.add(arr[i] + arr[j]);
            }
        }

        a: for (int i = N-1; i >= 0; i--) {
            for (int j = 0; j <= i; j++) {
                if(sums.contains(arr[i] - arr[j])){
                    bw.write(arr[i] + "");
                    break a;
                }
            }
        }
        bw.close();
    }
}
```
