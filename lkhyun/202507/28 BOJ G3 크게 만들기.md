```java
import java.util.*;
import java.io.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N, K;

    public static void main(String[] args) throws Exception {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());
        
        String input = br.readLine();
        
        ArrayDeque<Character> deq = new ArrayDeque<>();
        int removeCount = K;
        
        for (int i = 0; i < N; i++) {
            char cur = input.charAt(i);
            
            while (!deq.isEmpty() && deq.peek() < cur && removeCount > 0) {
                deq.pop();
                removeCount--;
            }
            
            deq.push(cur);
        }
        
        while (removeCount > 0) {
            deq.pop();
            removeCount--;
        }
        
        StringBuilder sb = new StringBuilder();
        while(!deq.isEmpty()){
            sb.append(deq.pollLast());
        }
        
        bw.write(sb.toString());
        bw.close();
    }
}
```
