```java
import java.util.*;
import java.io.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N;

    public static void main(String[] args) throws Exception {
        N = Integer.parseInt(br.readLine());
        List<int[]> arr = new LinkedList<>();

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            arr.add(new int[]{Integer.parseInt(st.nextToken()),Integer.parseInt(st.nextToken())});
        }
        Collections.sort(arr,(a,b) -> a[0] - b[0]);

        PriorityQueue<Integer> pq = new PriorityQueue<>();

        int ans = 1;
        for (int[] cur : arr) {
            while(!pq.isEmpty() && pq.peek() <= cur[0]){
                pq.poll();
            }
            pq.offer(cur[1]);
            ans = Math.max(ans,pq.size());
        }
        bw.write(ans+"");
        bw.close();
    }
}
```
