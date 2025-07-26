```java
import java.util.*;
import java.io.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int[] arr;
    static int[] NGE;

    public static void main(String[] args) throws Exception {
        int N = Integer.parseInt(br.readLine());
        arr = new int[N];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }
        if(N == 1){
            bw.write("-1");
            bw.close();
            return;
        }

        NGE = new int[N];
        ArrayDeque<Integer> stk = new ArrayDeque<>();
        stk.push(0);
        for (int i = 1; i < N; i++) {
            while(!stk.isEmpty() && arr[stk.peek()]<arr[i]){
                NGE[stk.poll()] = arr[i];
            }
            stk.push(i);
        }
        while(!stk.isEmpty()){
            NGE[stk.poll()] = -1;
        }
        for (int i = 0; i < N; i++) {
            bw.write(NGE[i]+" ");
        }
        bw.close();
    }
}
```
