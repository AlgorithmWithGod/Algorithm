```java
import java.util.*;
import java.io.*;

public class Main {
    static class Node{
        int value,idx;
        Node(int value, int idx){
            this.value = value;
            this.idx = idx;
        }
    }
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringBuilder sb = new StringBuilder();
    static StringTokenizer st;
    static int N,L;
    static ArrayDeque<Node> deq = new ArrayDeque<>();
    public static void main(String[] args) throws Exception {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        L = Integer.parseInt(st.nextToken());

        st = new StringTokenizer(br.readLine());
        for(int i = 0; i < N; i++){            
            Node cur = new Node(Integer.parseInt(st.nextToken()), i);
            while(!deq.isEmpty() && deq.peekLast().value > cur.value) deq.pollLast();
            deq.offer(cur);
            while(deq.peekFirst().idx < i-L+1) deq.poll();
            bw.write(deq.peekFirst().value+" ");
        }
        bw.close();
    }
}
```
