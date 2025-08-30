```java
import java.io.*;
import java.util.*;

public class Main {

    static int cnt,ans;
    static int[] arr;

    public static void main(String[] args) throws Exception {
        init();
        process();
        print();

    }

    public static void init() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        cnt = Integer.parseInt(br.readLine());
        arr = new int[cnt];
        for (int i = 0; i < cnt; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            st.nextToken();
            arr[i] = Integer.parseInt(st.nextToken());
        }
        ans = 0;
    }

    public static void process(){
        PriorityQueue<Integer> pq = new PriorityQueue<>(Collections.reverseOrder());
        for (int i = 0; i < cnt; i++) {
            int height = arr[i];

            while (!pq.isEmpty() && pq.peek() > height) {
                pq.poll();
                ans++;
            }

            if (height == 0) continue;

            if (pq.isEmpty() ||  pq.peek() != height) pq.add(height);


        }

        ans += pq.size();
    }

    public static void print(){
        System.out.println(ans);
    }


}
```
