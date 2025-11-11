```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringBuilder sb = new StringBuilder();
    static int N;
    static PriorityQueue<Integer> minheap = new PriorityQueue<>();
    static PriorityQueue<Integer> maxheap = new PriorityQueue<>(Comparator.reverseOrder());
    public static void main(String[] args) throws Exception {
        N = Integer.parseInt(br.readLine());

        for(int i = 0; i<N; i++){
            maxheap.offer(Integer.parseInt(br.readLine()));
            minheap.offer(maxheap.poll());
            if(maxheap.size()< minheap.size()){
                maxheap.offer(minheap.poll());
            }
            bw.write(maxheap.peek()+"\n");
        }
        bw.close();
    }
}
```
