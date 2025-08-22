```java
import java.util.*;
import java.io.*;

public class boj21924 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
    static int nextInt() {return Integer.parseInt(st.nextToken());}

    static int N, M, cnt = 0;
    static long answer;
    static ArrayList<ArrayList<Node>> graph = new ArrayList<>();
    static boolean[] visited;
    public static void main(String[] args) throws Exception {
        nextLine();
        N = nextInt();
        M = nextInt();
        visited = new boolean[N+1];
        for (int i = 0; i <= N; i++) graph.add(new ArrayList<Node>());
        for (int i = 0; i < M; i++) {
            nextLine();
            int a = nextInt();
            int b = nextInt();
            int c = nextInt();
            graph.get(a).add(new Node(b, c));
            graph.get(b).add(new Node(a, c));
            answer += c;
        }
        dijkstra();

        if (cnt == N) System.out.println(answer);
        else System.out.println(-1);
    }

    static void dijkstra() {
        PriorityQueue<Node> pq = new PriorityQueue<>((o1,o2) -> o1.c-o2.c);
        pq.offer(new Node(1, 0));

        while(!pq.isEmpty()) {
            Node cur = pq.poll();
            if (visited[cur.v]) continue;
            visited[cur.v] = true;
            answer -= cur.c;
            cnt++;
            for (Node next : graph.get(cur.v)) {
                if (visited[next.v]) continue;
                pq.offer(next);
            }
        }
    }

    static class Node {
        int v, c;
        public Node(int v, int c) {
            this.v = v;
            this.c = c;
        }
    }
}
```
