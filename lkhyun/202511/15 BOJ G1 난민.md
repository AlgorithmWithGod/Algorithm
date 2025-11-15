```java
import java.util.*;
import java.io.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringBuilder sb = new StringBuilder();
    static StringTokenizer st;
    static int N;

    static PriorityQueue<Long> minheap = new PriorityQueue<>();
    static PriorityQueue<Long> maxheap = new PriorityQueue<>(Comparator.reverseOrder());
    public static void main(String[] args) throws Exception {
        N = Integer.parseInt(br.readLine());
        long prevY = 0;
        long accumulation = 0; //누적 이동거리
        for(int i = 1; i <= N; i++){
            st = new StringTokenizer(br.readLine());
            long curX = Long.parseLong(st.nextToken());
            long curY = Long.parseLong(st.nextToken());

            maxheap.add(curY); //일단 maxheap에 넣음.
            minheap.add(maxheap.poll());
            if(maxheap.size() < minheap.size()){
                maxheap.add(minheap.poll());
            }
            if(i % 2 == 0){
                accumulation += (Math.abs(curX) + Math.abs(prevY - curY));
                prevY = maxheap.peek();
            }else{
                prevY = maxheap.peek();
                accumulation += (Math.abs(curX) + Math.abs(prevY - curY));
            }
            bw.write(prevY + " " + accumulation + "\n");
        }
        bw.close();
    }
}
```
