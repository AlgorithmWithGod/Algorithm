```java
import java.util.*;
import java.io.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int[] arr;
    static Map<Integer,Integer> count;
    static int[] NGF;

    public static void main(String[] args) throws Exception {
        int N = Integer.parseInt(br.readLine());
        arr = new int[N];
        count = new HashMap<>();
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
            count.put(arr[i], count.getOrDefault(arr[i], 0)+1);
        }
        if(N == 1){
            bw.write("-1");
            bw.close();
            return;
        }

        NGF = new int[N];
        ArrayDeque<Integer> stk = new ArrayDeque<>();
        stk.push(0);
        for (int i = 1; i < N; i++) {
            while(!stk.isEmpty() && count.get(arr[stk.peek()])<count.get(arr[i])){
                NGF[stk.poll()] = arr[i];
            }
            stk.push(i);
        }
        while(!stk.isEmpty()){
            NGF[stk.poll()] = -1;
        }
        for (int i = 0; i < N; i++) {
            bw.write(NGF[i]+" ");
        }
        bw.close();
    }
}
```
