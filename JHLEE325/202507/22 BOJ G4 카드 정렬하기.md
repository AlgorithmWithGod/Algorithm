```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.*;

public class Main {

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int n = Integer.parseInt(br.readLine());
        Queue<Integer> q = new PriorityQueue<>();

        for (int i = 0; i < n; i++) {
            q.add(Integer.parseInt(br.readLine()));
        }

        int result = 0;
        while (q.size() != 1) {
            int a = q.poll();
            int b = q.poll();
            result += a + b;
            q.add(a + b);
        }

        System.out.println(result);
    }
}

```
