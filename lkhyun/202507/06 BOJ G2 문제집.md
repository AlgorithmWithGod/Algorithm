```java
import java.util.*;
import java.io.*;
public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N,M;
    static List<Integer>[] adj;
    static int[] degree;

    public static void main(String[] args) throws IOException {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        adj = new List[N+1];
        degree = new int[N+1];

        for (int i = 1; i <= N; i++) {
            adj[i] = new ArrayList<>();
        }

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            adj[a].add(b);
            degree[b]++;
        }


        BFS();
        bw.close();
    }
    static void BFS() throws IOException {
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        for (int i = 1; i <= N; i++) {
            if(degree[i] == 0){
                pq.add(i);
            }
        }

        while(!pq.isEmpty()){
            int u = pq.poll();
            bw.write(u+" ");

            for(int v : adj[u]){
                if(--degree[v] == 0){
                    pq.add(v);
                }
            }
        }
    }
}

```
