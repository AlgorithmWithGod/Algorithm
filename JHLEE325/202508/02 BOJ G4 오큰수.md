```java
import java.io.*;
import java.util.*;

public class Main {

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int n = Integer.parseInt(br.readLine());
        int[] arr = new int[n];
        int[] result = new int[n];
        Stack<Integer> stk = new Stack<>();

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < n; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }

        for (int i = n - 1; i >= 0; i--) {
            while (!stk.isEmpty()) {
                if (stk.peek() > arr[i]) {
                    result[i] = stk.peek();
                    break;
                } else stk.pop();
            }
            if (stk.isEmpty()) result[i] = -1;
            stk.push(arr[i]);
        }

        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < n; i++) {
            sb.append(result[i] + " ");
        }

        System.out.println(sb.toString());
    }
}

```
