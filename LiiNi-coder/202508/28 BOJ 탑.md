```java
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.util.Stack;
import java.util.StringTokenizer;

public class Main{
    private static BufferedReader Br;
    private static int N;
    private static int[] Arr;
    private static final int MAX = 100_000_001;
    private static BufferedWriter Bw;
    private static StringBuilder Sb;

    public static void main(String[] args) throws IOException {
        Br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(Br.readLine());
        Bw = new BufferedWriter(new OutputStreamWriter(System.out));
        Sb = new StringBuilder();
        Arr = new int[N + 1];
        StringTokenizer st = new StringTokenizer(Br.readLine());
        for(int i = 0; i < N; i++){
            Arr[i+1] = Integer.parseInt(st.nextToken());
        }

        Stack<int[]> stack = new Stack<>();
        stack.add(new int[]{MAX, 0});
        for (int i = 1; i <= N; i++) {
            while (!stack.isEmpty() && stack.peek()[0] < Arr[i]) {
                stack.pop();
            }
            // stack.peek()[1] == 0 이면, 수신할 탑 없음
            p(stack.peek()[1]);
            stack.add(new int[]{Arr[i], i});
        }
        Bw.write(Sb.toString() + "\n");
        Bw.flush();
        Bw.close();
        Br.close();
    }

    private static void p(int i){
        Sb.append(i + " ");
    }
}
```
