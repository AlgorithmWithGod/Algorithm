```java
import java.util.*;
import java.io.*;

class Solution
{
    static ArrayList<ArrayList<Point>> graph;
    static int[] answer;

    public static void main(String[] args) throws Exception{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int p = Integer.parseInt(st.nextToken());
        int w = Integer.parseInt(st.nextToken());
        st = new StringTokenizer(br.readLine());
        int c = Integer.parseInt(st.nextToken());
        int v = Integer.parseInt(st.nextToken());
        answer = new int[p];
        graph = new ArrayList<>(p+1);
        
        for (int i = 0; i < p; i++) {
            graph.add(new ArrayList<Point>());
        }

        for (int i = 0; i < w; i++) {
            st = new StringTokenizer(br.readLine());
            int start = Integer.parseInt(st.nextToken());
            int end = Integer.parseInt(st.nextToken());
            int weight = Integer.parseInt(st.nextToken());

            graph.get(start).add(new Point(end, weight));
            graph.get(end).add(new Point(start, weight));
        }

        bfs(c, v);
        System.out.println(answer[v]);
    }

    static void bfs(int from, int to) {
        Queue<Point> q = new LinkedList<>();
        q.offer(new Point(from, 0));
        answer[from] = Integer.MAX_VALUE;
        while (!q.isEmpty()) {
            Point curr = q.poll();
            if (curr.e == to) continue;
            for (Point next : graph.get(curr.e)) {
            	int nextWieght = Math.min(answer[curr.e], next.w);
                if (answer[next.e] >= nextWieght) continue;
                answer[next.e] = nextWieght;
                q.offer(new Point(next.e, nextWieght));
            }
        }
    }

    static class Point {
        int e;
        int w;
        public Point(int e, int w) {
            this.e = e;
            this.w = w;
        }
    }
}

```
