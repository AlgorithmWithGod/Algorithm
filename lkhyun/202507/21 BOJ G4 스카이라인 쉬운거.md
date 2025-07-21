```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N;
    static int ans = 0;
    public static void main(String[] args) throws Exception {
        N = Integer.parseInt(br.readLine());

        ArrayDeque<Integer> stk = new ArrayDeque<>();
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            int x = Integer.parseInt(st.nextToken());
            int y = Integer.parseInt(st.nextToken());

            while(!stk.isEmpty() && stk.peek() > y){
                stk.pop();
                ans++;
            }
            if(stk.isEmpty() && y > 0){
                stk.push(y);
            }else if(!stk.isEmpty() && stk.peek() < y){
                stk.push(y);
            }
        }
        ans += stk.size();
        bw.write(ans + "\n");
        bw.close();
    }
}
```
