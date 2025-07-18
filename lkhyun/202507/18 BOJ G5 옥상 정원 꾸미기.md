```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static int N;
    static int[] buildings;
    static long ans = 0;
    public static void main(String[] args) throws Exception {
        N = Integer.parseInt(br.readLine());
        buildings = new int[N];

        for (int i = 0; i < N; i++) {
            buildings[i] = Integer.parseInt(br.readLine());
        }

        ArrayDeque<Integer> key = new ArrayDeque<>();
        ArrayDeque<Integer> value = new ArrayDeque<>();
        key.push(0);
        value.push(buildings[0]);
        for (int i = 1; i < N; i++) {
            while(!key.isEmpty() && buildings[i] >= value.peek()){
                value.pop();
                ans += i - key.pop() - 1;
            }
            key.push(i);
            value.push(buildings[i]);
        }
        while(!key.isEmpty()){
            ans += N - key.pop() - 1;
        }
        bw.write(ans+"");
        bw.close();
    }
}
```
