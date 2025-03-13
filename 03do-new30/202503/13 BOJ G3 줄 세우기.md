```java
import java.util.*;
import java.io.*;

public class Main {
    static int N, M;
    static List<Integer>[] graph;
    static int[] indegree;
    public static void main(String[] args) throws IOException {
        input();
        getIndegree();
        List<Integer> order = topologySort();
        for (int num : order) {
            System.out.print(num + " ");
        }
        System.out.println();
    }

    static ArrayList<Integer> topologySort() {
        ArrayList<Integer> orderList = new ArrayList<>(); // 정점의 방문 순서
        Queue<Integer> q = new ArrayDeque<>();
        for (int i = 1; i < N+1; i++) {
            if (indegree[i] == 0) {
                q.offer(i);
            }
        }

        while (!q.isEmpty()) {
            int node = q.poll();
            orderList.add(node);
            for (int next : graph[node]) {
                if (--indegree[next] == 0) q.offer(next);
            }
        }
        return orderList;
    }

    static void getIndegree() {
        indegree = new int[N+1];
        for (int from = 1; from < N+1; from++) {
            for (int to : graph[from] ){
                // 진입 차수 기록
                indegree[to]++;
            }
        }
    }

    static void input() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        graph = new List[N+1];
        for (int i = 1; i < N+1; i++) {
            graph[i] = new ArrayList<>();
        }
        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            graph[a].add(b);
        }
        br.close();

    }
}
```
