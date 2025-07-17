```java
import java.util.*;
import java.io.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N,M;
    static int[] arr;
    static int[][] manipulation;
    static int[] correct;
    static int ans = -1;

    public static void main(String[] args) throws Exception {
        N = Integer.parseInt(br.readLine());
        arr = new int[N+1];

        st = new StringTokenizer(br.readLine());
        for (int i = 1; i <= N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }
        correct = Arrays.copyOf(arr, N+1);
        Arrays.sort(correct);

        M = Integer.parseInt(br.readLine());
        manipulation = new int[M][3];

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            int c = Integer.parseInt(st.nextToken());
            manipulation[i] = new int[]{a,b,c};
        }

        dijkstra();

        bw.write(ans+"");
        bw.close();
    }
    static void dijkstra(){
        PriorityQueue<int[]> pq = new PriorityQueue<>((a,b) -> a[0]-b[0]);
        Map<String, Integer> dist =  new HashMap<>();
        pq.offer(arr);
        dist.put(Arrays.toString(Arrays.copyOfRange(arr,1,N+1)),0);

        while (!pq.isEmpty()){
            int[] cur = pq.poll();
            String curString = Arrays.toString(Arrays.copyOfRange(cur,1,N+1));

            if(dist.get(curString) < cur[0]) continue;

            for(int i = 0; i<M; i++){
                int[] next = Arrays.copyOf(cur,N+1);
                next[manipulation[i][1]] = cur[manipulation[i][0]];
                next[manipulation[i][0]] = cur[manipulation[i][1]];
                int newDist = dist.get(curString) + manipulation[i][2];
                next[0] = newDist;
                String nextString = Arrays.toString(Arrays.copyOfRange(next,1,N+1));
                if(dist.get(nextString) == null || newDist < dist.get(nextString)){
                    dist.put(nextString, newDist);
                    pq.offer(next);
                }
            }
        }
        ans = dist.getOrDefault(Arrays.toString(Arrays.copyOfRange(correct,1,N+1)), -1);
    }
}
```
