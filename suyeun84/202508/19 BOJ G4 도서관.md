```java
import java.util.*;
import java.io.*;

public class boj1461 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
    static int nextInt() {return Integer.parseInt(st.nextToken());}

    public static void main(String[] args) throws Exception {
        nextLine();
        int N = nextInt();
        int M = nextInt();
        int answer = 0;
        PriorityQueue<Integer> pos = new PriorityQueue<>(Collections.reverseOrder());
        PriorityQueue<Integer> neg = new PriorityQueue<>(Collections.reverseOrder());
        nextLine();
        for (int i = 0; i < N; i++) {
            int num = nextInt();
            if (num < 0) neg.add(Math.abs(num));
            else pos.add(num);
        }
        int last = 0;
        if (pos.isEmpty()) last = neg.peek();
        else if (neg.isEmpty()) last = pos.peek();
        else {
            last = Math.max(neg.peek(), pos.peek());
        }

        while (!pos.isEmpty()) {
            answer += pos.peek() * 2;
            for (int i = 0; i < M; i++) pos.poll();
        }

        while(!neg.isEmpty()) {
            answer += neg.peek() * 2;
            for (int i = 0; i < M; i++) neg.poll();
        }

        System.out.println(answer - last);
    }
}
```
