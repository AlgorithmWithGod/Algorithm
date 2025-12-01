```java
import java.io.*;
import java.util.*;

public class Main {

    static class City implements Comparable<City> {
        int number;
        int cost;

        City(int number, int cost) {
            this.number = number;
            this.cost = cost;
        }

        @Override
        public int compareTo(City other) {
            return Integer.compare(this.cost, other.cost);
        }
    }

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int n = Integer.parseInt(br.readLine());
        int m = Integer.parseInt(br.readLine()); 

        List<City>[] graph = new ArrayList[n + 1];
        for (int i = 1; i <= n; i++) {
            graph[i] = new ArrayList<>();
        }

        for (int i = 0; i < m; i++) {
            st = new StringTokenizer(br.readLine());
            int from = Integer.parseInt(st.nextToken());
            int to   = Integer.parseInt(st.nextToken());
            int cost = Integer.parseInt(st.nextToken());

            graph[from].add(new City(to, cost));
        }

        st = new StringTokenizer(br.readLine());
        int start = Integer.parseInt(st.nextToken());
        int end   = Integer.parseInt(st.nextToken());

        int[] dist = new int[n + 1];
        boolean[] visited = new boolean[n + 1];
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[start] = 0;

        PriorityQueue<City> pq = new PriorityQueue<>();
        pq.offer(new City(start, 0));

        while (!pq.isEmpty()) {
            City cur = pq.poll();
            int now = cur.number;
            int costSoFar = cur.cost;

            if (visited[now]) continue;
            visited[now] = true;

            for (City next : graph[now]) {
                int nextCity = next.number;
                int nextCost = costSoFar + next.cost;

                if (!visited[nextCity] && dist[nextCity] > nextCost) {
                    dist[nextCity] = nextCost;
                    pq.offer(new City(nextCity, nextCost));
                }
            }
        }

        System.out.println(dist[end]);
    }
}

```
