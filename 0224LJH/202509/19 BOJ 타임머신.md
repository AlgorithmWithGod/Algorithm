```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

class Main {
    
    static int N, M, a, b, c;
    static List<List<Integer>> graph;
    static List<List<Integer>> reverseGraph;
    static final long INF = Long.MAX_VALUE / 2;
    
    static class Node implements Comparable<Node> {
        int num;
        long cost;
        
        public Node(int num, long cost) {
            this.num = num;
            this.cost = cost;
        }
        
        @Override
        public int compareTo(Node n) {
            return Long.compare(this.cost, n.cost);
        }
    }
    
    public static void main(String[] args) throws NumberFormatException, IOException {
        init();
        process();
    }
    
    public static void init() throws NumberFormatException, IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        a = Integer.parseInt(st.nextToken());
        b = Integer.parseInt(st.nextToken());
        c = Integer.parseInt(st.nextToken());
        
        graph = new ArrayList<>();
        reverseGraph = new ArrayList<>();
        
        for (int i = 0; i <= N; i++) {
            graph.add(new ArrayList<>());
            reverseGraph.add(new ArrayList<>());
        }
        
        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int u = Integer.parseInt(st.nextToken());
            int v = Integer.parseInt(st.nextToken());
            
            graph.get(u).add(v);
            reverseGraph.get(v).add(u);
        }
    }
    
    public static void process() {
        // 1. 타임머신을 고려한 수정된 다익스트라
        long[] dist = modifiedDijkstra();
        
        // 2. 결과 출력
        if (dist[N] == INF) {
            System.out.println("x");
        } else if (dist[N] <= -INF/2) {  // 음의 무한대로 발산
            System.out.println("-inf");
        } else {
            System.out.println(dist[N]);
        }
    }
    
    public static long[] modifiedDijkstra() {
        long[] dist = new long[N + 1];
        Arrays.fill(dist, INF);
        
        // 타임머신 사이클 비용 계산을 위한 BFS
        int distBtoA = bfs(b, a);
        boolean cyclePossible = (distBtoA != -1);
        long cycleCost = cyclePossible ? (distBtoA - c) : 0;
        
        // N에서 역방향으로 도달 가능한 노드들 찾기
        boolean[] reachableFromN = new boolean[N + 1];
        findReachable(N, reverseGraph, reachableFromN);
        
        PriorityQueue<Node> pq = new PriorityQueue<>();
        dist[1] = 0;
        pq.add(new Node(1, 0));
        
        // 음의 사이클 체크를 위한 방문 횟수 카운트
        int[] visitCount = new int[N + 1];
        
        while (!pq.isEmpty()) {
            Node cur = pq.poll();
            
            // 너무 많이 방문했으면 음의 사이클
            if (visitCount[cur.num] > N) {
                if (reachableFromN[cur.num]) {
                    dist[N] = -INF;
                    return dist;
                }
                continue;
            }
            
            visitCount[cur.num]++;
            
            // 일반 간선 처리
            for (int next : graph.get(cur.num)) {
                long newCost = dist[cur.num] + 1;
                if (newCost < dist[next]) {
                    dist[next] = newCost;
                    pq.add(new Node(next, newCost));
                }
            }
            
            // 타임머신 처리 (a번 정점에서만)
            if (cur.num == a) {
                long newCost = dist[a] - c;
                if (newCost < dist[b]) {
                    dist[b] = newCost;
                    pq.add(new Node(b, newCost));
                    
                    // 음의 사이클 감지
                    if (cyclePossible && cycleCost < 0 && reachableFromN[a]) {
                        dist[N] = -INF;
                        return dist;
                    }
                }
            }
        }
        
        return dist;
    }
    
    // BFS로 최단 거리 찾기 (가중치가 모두 1이므로)
    public static int bfs(int start, int end) {
        if (start == end) return 0;
        
        Queue<Integer> q = new LinkedList<>();
        int[] dist = new int[N + 1];
        Arrays.fill(dist, -1);
        
        q.add(start);
        dist[start] = 0;
        
        while (!q.isEmpty()) {
            int cur = q.poll();
            
            for (int next : graph.get(cur)) {
                if (dist[next] == -1) {
                    dist[next] = dist[cur] + 1;
                    q.add(next);
                    
                    if (next == end) {
                        return dist[next];
                    }
                }
            }
        }
        
        return -1;
    }
    
    // 특정 노드에서 도달 가능한 모든 노드 찾기
    public static void findReachable(int start, List<List<Integer>> g, boolean[] reachable) {
        Queue<Integer> q = new LinkedList<>();
        q.add(start);
        reachable[start] = true;
        
        while (!q.isEmpty()) {
            int cur = q.poll();
            
            for (int next : g.get(cur)) {
                if (!reachable[next]) {
                    reachable[next] = true;
                    q.add(next);
                }
            }
        }
    }
}
```
