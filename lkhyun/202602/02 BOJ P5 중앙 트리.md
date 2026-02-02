```java
import java.util.*;
import java.io.*;

public class Main {
    static class Node{
        int to, weight;
        Node(int to, int weight){
            this.to = to;
            this.weight = weight;
        }
    }
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static List<Node>[] adjList;
    static int[] subTreeCnt;
    static long[] totalDistance;
    static boolean[] visited;


    public static void main(String[] args) throws Exception {
        while(true){
            int n = Integer.parseInt(br.readLine());
            long ans = Long.MAX_VALUE;
            if(n == 0) break;

            adjList = new List[n];
            for (int i = 0; i < n; i++) {
                adjList[i] = new ArrayList<>();
            }
            for (int i = 1; i < n; i++) {
                st = new StringTokenizer(br.readLine());
                int from = Integer.parseInt(st.nextToken());
                int to = Integer.parseInt(st.nextToken());
                int weight = Integer.parseInt(st.nextToken());
                adjList[from].add(new Node(to,weight));
                adjList[to].add(new Node(from,weight));
            }

            subTreeCnt = new int[n];
            totalDistance = new long[n];

            visited = new boolean[n];
            dfs(0);
            visited = new boolean[n];
            reRooting(0, n);

            for (int i = 0; i < n; i++) {
                ans = Math.min(ans,totalDistance[i]);
            }
            System.out.println(ans);
        }
    }
    public static void dfs(int start){
        if(visited[start]) return;

        visited[start] = true;

        for (Node next : adjList[start]) {
            if(visited[next.to]) continue;
            dfs(next.to);
            subTreeCnt[start] += subTreeCnt[next.to] + 1;
            totalDistance[start] += totalDistance[next.to] + ((long) (subTreeCnt[next.to] + 1) * next.weight);
        }
    }

    public static void reRooting(int start, int n){
        if(visited[start]) return;

        visited[start] = true;

        for (Node next : adjList[start]) {
            if(visited[next.to]) continue;
            totalDistance[next.to] = totalDistance[start] + ((n - (subTreeCnt[next.to]+1)* 2L) * next.weight);
            reRooting(next.to,n);
        }
    }
}
```
