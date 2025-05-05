```java
import java.io.*;
import java.util.*;

public class Main {
    static class Node {
        int to,cost;
        Node(int to, int cost) {
            this.to = to;
            this.cost = cost;
        }
    }
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N;
    static List<Node>[] adjList;

    public static void main(String[] args) throws Exception {
        N = Integer.parseInt(br.readLine());
        if(N == 1){
            bw.write("0");
            bw.close();
            return;
        }
        adjList = new ArrayList[N+1];
        for (int i = 1; i <= N; i++) {
            adjList[i] = new ArrayList<>();
        }
        for (int i = 1; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            int p = Integer.parseInt(st.nextToken());
            int c = Integer.parseInt(st.nextToken());
            int w = Integer.parseInt(st.nextToken());
            adjList[p].add(new Node(c, w));
            adjList[c].add(new Node(p, w));
        }
        int[] dist = new int[N+1];
        int A = BFS(1,dist);
        int B = BFS(A,dist);
        bw.write(dist[B]+"");
        bw.close();
    }
    public static int BFS(int start,int[] dist){
        Arrays.fill(dist, Integer.MAX_VALUE);
        Queue<Integer> q = new ArrayDeque<>();
        q.add(start);
        dist[start] = 0;

        int destination = start;
        while(!q.isEmpty()){
            int cur = q.poll();
            for(Node node : adjList[cur]){
                if(dist[node.to] == Integer.MAX_VALUE){
                    dist[node.to] = dist[cur] + node.cost;
                    q.add(node.to);
                    if(dist[node.to] > dist[destination]) destination = node.to;
                }
            }
        }
        return destination;
    }
}
```
