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
    static int N,E;
    static List<Node>[] adjList;
    static int v1,v2;
    static int MAX = Integer.MAX_VALUE;
    static int min = -1;

    public static void main(String[] args) throws Exception {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        E = Integer.parseInt(st.nextToken());
        adjList = new ArrayList[N+1];
        for (int i = 1; i <= N; i++) {
            adjList[i] = new ArrayList<>();
        }
        for (int i = 0; i < E; i++) {
            st = new StringTokenizer(br.readLine());
            int from = Integer.parseInt(st.nextToken());
            int to = Integer.parseInt(st.nextToken());
            int cost = Integer.parseInt(st.nextToken());
            adjList[from].add(new Node(to, cost));
            adjList[to].add(new Node(from, cost));
        }
        st = new StringTokenizer(br.readLine());
        v1 = Integer.parseInt(st.nextToken());
        v2 = Integer.parseInt(st.nextToken());
        int[][] dist = new int[3][N+1];
        dijkstra(1,dist[0]);
        dijkstra(v1,dist[1]);
        dijkstra(v2,dist[2]);

        boolean flag1 = true;
        boolean flag2 = true;
        if(dist[0][v1] == MAX || dist[1][v2] == MAX || dist[2][N] == MAX) flag1 = false;
        if(dist[0][v2] == MAX || dist[2][v1] == MAX || dist[1][N] == MAX) flag2 = false;
        if(flag1 && flag2){
            min = Math.min(dist[0][v1] + dist[1][v2] + dist[2][N],dist[0][v2] + dist[2][v1] + dist[1][N]);
        }else if(flag1){
            min = dist[0][v1] + dist[1][v2] + dist[2][N];
        }else if(flag2){
            min = dist[0][v2] + dist[2][v1] + dist[1][N];
        }
        bw.write(min + "");
        bw.close();
    }
    public static void dijkstra(int start , int[] dist) {
        PriorityQueue<Node> pq = new PriorityQueue<>((a,b) -> a.cost - b.cost);
        pq.add(new Node(start,0));
        Arrays.fill(dist,MAX);
        dist[start] = 0;

        while (!pq.isEmpty()) {
            Node cur = pq.poll();

            if(cur.cost > dist[cur.to]) {
                continue;
            }
            for(Node n : adjList[cur.to]){
                int newDist = dist[cur.to] + n.cost;
                if(newDist < dist[n.to]) {
                    dist[n.to] = newDist;
                    pq.add(new Node(n.to,newDist));
                }
            }
        }
    }

}
```
