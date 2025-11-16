```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int N = Integer.parseInt(st.nextToken());
        int[] arr = new int[N];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }

        int mnum = 1000000;
        int[] count = new int[mnum + 1];
        for (int i = 0; i < N; i++) {
            count[arr[i]]++;
        }

        int[] result = new int[N];
        Stack<Integer> stack = new Stack<>();

        for (int i = N - 1; i >= 0; i--) {
            int f = count[arr[i]];
            while (!stack.isEmpty() && count[stack.peek()] <= f) {
                stack.pop();
            }
            if (stack.isEmpty()) {
                result[i] = -1;
            } else {
                result[i] = stack.peek();
            }
            stack.push(arr[i]);
        }

        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < N; i++) {
            sb.append(result[i]).append(' ');
        }
        System.out.println(sb.toString());
    }
}
```
