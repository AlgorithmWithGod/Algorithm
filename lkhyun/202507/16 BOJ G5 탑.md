```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N;
    static int[] tops;
    static int[] reception;

    public static void main(String[] args) throws Exception {
        N = Integer.parseInt(br.readLine());
        st = new StringTokenizer(br.readLine());
        tops = new int[N+1];
        reception = new int[N+1];

        for (int i = 1; i <= N; i++) {
            tops[i] = Integer.parseInt(st.nextToken());
        }

        ArrayDeque<int[]> stack = new ArrayDeque<>();
        stack.push(new int[]{tops[N],N});

        for (int i = N-1; i >= 1; i--) {
            while(!stack.isEmpty() && tops[i] > stack.peek()[0]){
                int[] top = stack.pop();
                reception[top[1]] = i;
            }
            stack.push(new int[]{tops[i],i});
        }

        StringBuilder sb = new StringBuilder();
        for (int i = 1; i <= N; i++) {
            sb.append(reception[i]);
            if(i != N){
                sb.append(" ");
            }
        }
        bw.write(sb.toString());
        bw.close();
    }
}
```
