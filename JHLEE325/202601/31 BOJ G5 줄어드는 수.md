```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        
        int N = Integer.parseInt(br.readLine());

        if (N == 1) {
            System.out.println(0);
            return;
        }

        Queue<Long> queue = new LinkedList<>();
        for (int i = 1; i <= 9; i++) {
            queue.add((long) i);
        }

        int count = 1;

        while (!queue.isEmpty()) {
            long current = queue.poll();
            count++;

            if (count == N) {
                System.out.println(current);
                return;
            }

            long lastDigit = current % 10;
            
            for (int i = 0; i < lastDigit; i++) {
                long nextNum = (current * 10) + i;
                queue.add(nextNum);
            }
        }

        System.out.println("-1");
    }
}
```
