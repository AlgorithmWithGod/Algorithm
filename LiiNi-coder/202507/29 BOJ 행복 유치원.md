```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.PriorityQueue;
import java.util.StringTokenizer;
import java.util.Comparator;

public class Main {

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int N = Integer.parseInt(st.nextToken());
        int K = Integer.parseInt(st.nextToken());

        int[] height = new int[N];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            height[i] = Integer.parseInt(st.nextToken());
        }

        int[] diffs = new int[N - 1];
        for (int i = 0; i < N - 1; i++) {
            diffs[i] = height[i + 1] - height[i];
        }
        //자바는 기본이 minheap이라서 이렇게 comparator를 두어야한다
        PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Comparator.reverseOrder());

        int total = 0;
        for (int d : diffs) {
            total += d;
            maxHeap.offer(d);
        }
        for (int i = 0; i < K - 1; i++) {
            total -= maxHeap.poll();
        }
        System.out.println(total);
    }
}
```
