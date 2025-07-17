```java
import java.util.*;
import java.io.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str = br.readLine();
        String target = br.readLine();
        int n = str.length();
        int m = target.length();
        Deque<Character> deque = new ArrayDeque<>();

        for (int i = 0; i < n; i++) {
            deque.offerFirst(str.charAt(i));
            int idx = m-1;
            Deque<Character> tmp = new ArrayDeque<>();
            while (!deque.isEmpty() && idx >= 0 && deque.peekFirst() == target.charAt(idx)) {
                tmp.offerFirst(deque.pollFirst());
                idx--;
            }
            if (tmp.size() != m) {
                while(!tmp.isEmpty()) {
                    deque.offerFirst(tmp.pollFirst());
                }
            }
        }

        if (deque.isEmpty()) {
            System.out.println("FRULA");
        } else {
            StringBuilder sb = new StringBuilder();
            while (!deque.isEmpty()) {
                sb.append(deque.pollLast());
            }
            System.out.println(sb);
        }
        br.close();
    }
}
```
