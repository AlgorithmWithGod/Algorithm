```java
import java.io.*;
import java.util.*;

public class Main {
    static int n, m, r, maxItem;
    static int[] items;
    static List<int[]>[] graph;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());
        r = Integer.parseInt(st.nextToken());
        items = new int[n+1];
        st = new StringTokenizer(br.readLine());
        for (int i = 1; i <= n; i++) {
            items[i] =  Integer.parseInt(st.nextToken());
        }
        graph = new List[n+1];
        for (int i = 1; i <= n; i++) {
            graph[i] = new ArrayList<>();
        }
        for (int i = 0; i < r; i++) {
            st = new StringTokenizer(br.readLine());
            int a =  Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            int length = Integer.parseInt(st.nextToken());
            graph[a].add(new int[] {b, length});
            graph[b].add(new int[] {a, length});
        }

        for (int start = 1; start <= n; start++) {
            dijkstra(start);
        }
        System.out.println(maxItem);
        br.close();
    }

    private static void dijkstra(int start) {
        PriorityQueue<int[]> pq = new PriorityQueue<>(new Comparator<int[]>() {
            @Override
            public int compare(int[] o1, int[] o2) {
                return Integer.compare(o1[1], o2[1]);
            }
        });

        int[] dist = new int[n+1];
        for (int i = 1; i <= n; i++) {
            dist[i] = Integer.MAX_VALUE;
        }
        dist[start] = 0;
        pq.offer(new int[] {start, 0});

        while (!pq.isEmpty()) {
            int[] cur = pq.poll();
            int curNode = cur[0];
            for (int[] nex : graph[curNode]) {
                int nextNode = nex[0];
                int nextLength = nex[1];
                if (dist[nextNode] > dist[curNode] + nextLength) {
                    if (dist[curNode] + nextLength > m) {
                        continue;
                    }
                    dist[nextNode] = dist[curNode] + nextLength;
                    pq.offer(new int[]{nextNode, dist[nextNode]});
                }
            }
        }
        // 각 정점까지의 최단거리 구하기 완료
        // start 정점에서 출발했을 떄, 얻을 수 있는 최대 아이템 개수 출력
        int tmpItem = 0;
        for (int i = 1; i <= n; i++) {
            if (dist[i] == Integer.MAX_VALUE) { continue; }
            tmpItem += items[i];
        }
        maxItem = Math.max(tmpItem, maxItem);
    }
}
```
